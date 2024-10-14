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
```




* Reference: https://github.com/bitnami/containers/blob/main/bitnami/nginx/1.27/debian-12/Dockerfile
