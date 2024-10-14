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



* Reference: https://github.com/bitnami/containers/blob/main/bitnami/nginx/1.27/debian-12/Dockerfile
