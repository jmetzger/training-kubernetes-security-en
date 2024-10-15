# Privileges Escalation 

## Step 1: Building the image (Done by trainer already) 

  * https://gist.github.com/christophetd/a601618def2e3441fe680425cb7e1f4f

```
cd
mkdir builds
cd builds
mkdir escalate
cd escalate
```

```
nano Dockerfile
```

```
FROM alpine:3.20 AS builder
WORKDIR /build
RUN cat > escalate.c <<EOF
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <errno.h>

int main(void) {
    // Escalate to root
    setreuid(0, 0); setregid(0, 0);

    // Spawn a shell
    char* const argv[] = {"/bin/sh", NULL};
    char* const environ[] = {"PATH=/bin:/sbin:/usr/bin:/usr/sbin", NULL};
    if (-1 == execve("/bin/sh", argv, environ)) {
        printf("Unable to execve /bin/sh, errno %d\n", errno);
    }
}
EOF
RUN cat /build/escalate.c
RUN apk add --no-cache gcc musl-dev
RUN gcc escalate.c -Wall -o escalate

FROM alpine:3.20 AS runner
WORKDIR /app
COPY --from=builder /build/escalate ./escalate
RUN chown root:root ./escalate && chmod +s ./escalate
RUN adduser app-user --uid 1000 --system --disabled-password --no-create-home
USER app-user
ENTRYPOINT ["sh", "-c", "echo Application running && sleep infinity"]
```

```
docker build . -t dockertrainereu/escalate
docker push dockertrainereu/escalate 
```

## Step 2: Running pod with allowPrivilegeEscalation  

```
mkdir -p manifests
cd manifests
mkdir escalate-pod
cd escalate-pod
```

```
nano 01-pod.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: escalate
spec:
  securityContext:
    runAsUser: 10001
    runAsGroup: 10001
  containers:
  - name: escalate
    image: dockertrainereu/escalate 
    securityContext:
      allowPrivilegeEscalation: true
```

```
kubectl apply -f .
kubectl exec -it escalate -- sh
```

```
# Within shell
id
./escalate 
id
```

```
kubectl delete -f .
```

## Step 3: Running pod without allowPrivilegeEscalation  

```
nano 01-pod.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: escalate
spec:
  securityContext:
    runAsUser: 10001
    runAsGroup: 10001
  containers:
  - name: escalate
    image: dockertrainereu/escalate 
    securityContext:
      allowPrivilegeEscalation: false
```

```
kubectl apply -f .
kubectl exec -it escalate -- sh
```

```
# Within shell
id
./escalate 
id
```

```
kubectl delete -f .
```


## Step 4: What about: runAsNonroot 

```
nano 01-pod.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: escalate
spec:
  securityContext:
    runAsUser: 10001
    runAsGroup: 10001
    runAsNonRoot: true 
  containers:
  - name: escalate
    image: dockertrainereu/escalate 
    # securityContext:
    #   allowPrivilegeEscalation: # it is on by default
```

```
kubectl apply -f .
kubectl exec -it escalate -- sh
```

```
# Within shell
id
./escalate 
id
```





## Reference:

  * https://blog.christophetd.fr/stop-worrying-about-allowprivilegeescalation/
