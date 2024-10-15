# Exercise: Can we run bitnami/nginx - rootless, without capabilities ? 

## Step 1: Create manfifest and deploy 

```
cd
mkdir -p manifests
cd manifests
mkdir nonrootnginx
cd nonrootnginx
```

```
nano 01-pod.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-unpriv
spec:
  securityContext:
    runAsNonRoot: true 
  containers:
    - name: podmagic
      image: bitnami/nginx:1.27
      command: [ "sleep" ]
      args: [ "infinity" ]
      securityContext:
        allowPrivilegeEscalation: true 
        capabilities:
          drop:
          - all
```

```
kubectl apply -f .
kubectl get pods
kubect logs nginx-unpriv 
```

## Step 2: Conclusion 

  * It runs without any capabilities
  * It also runs as non-root
  * Downside: We cannot start a debug-container with root-prviliges because runAsNonRoot on spec.pod.securityContext  -> level 


## Step 3: Try to debug (does not work)

```
kubectl debug --it nginx-unpriv --image=alpine:1.20 
# cannot be start because of runNonRoot - Restrictions 
```

## Step 4: Prepare non-root - image for debugging (if necessary) 

```
# We have created an alpine image running as USER 1001
# vi Dockerfile
FROM alpine:1.20
USER 1001:1001
```

```
# ALREADY DONE FOR YOU
# And build an uploaded it to dockertrainereu (public)
docker build -t dockertrainereu/alpine-rootless:1.20 .
docker login
docker push dockertrainereu/alpine-rootless 
```


## Step 5: Use that new image (alpine-rootless) for debugging

```
kubectl debug -it nginx-unpriv --image=dockertrainereu/alpine-root
# you cannot ping of course. that is because of the nature, how ping is implemented in alpine -> busybox
```

```
# in container
id
ip a
wget -O - http://www.google.de 
```


* Reference: https://github.com/bitnami/containers/blob/main/bitnami/nginx/1.27/debian-12/Dockerfile


## Step 6: Use image to ping 

```
# just for information. This was created like so
# vi Dockerfile
FROM debian
RUN apt update -y && apt install -y iputils-ping && apt clean -y
USER 1001
```

```
# Let it run, start the game 
kubectl run -it debug nginx-unpriv --image=dockertrainereu/pinger-rootless
```


```
# in container
ping www.google.de
cat /proc/1/status | grep -i cap
# take the line with data
# now you can see the set capabilities 
capsh --decode=00000000a80435fb
```
