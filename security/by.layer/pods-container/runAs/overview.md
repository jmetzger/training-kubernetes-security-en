# runAs 

  * Best practices. Set on level of the pod
  * This also reflects containers that are started with kubectl debug (ephemerla containers)


## runAsUser 

  * Important: UID does not need to exist in container 
  * Really run as specific user.
  * If not set the user from Dockerfile is taken
  * Recommended to set it, that will be deep defense line
    * If image has a root user or can not run as root this will fail 

## Execrcise 

```
cd
mkdir -p manifests
cd manifests
mkdir run1
cd run1
```

```
nano 01-pod.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: pod
  name: nginxrun
spec:
  securityContext:
    runAsUser: 1001
  containers:
  - image: nginx:1.23
    name: pod
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```

```
kubectl apply -f 01-pod.yaml
kubectl describe pod nginxrun
kubectl logs nginxrun 
```


## runAsGroup 

  * Recommended to set this as well 

## runAsNonRoot 

  * Indicates that use must run as none root
  * If this is not configure in the image, the start fails
