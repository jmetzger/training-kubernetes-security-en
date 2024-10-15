# Start pod without capabilities 

```
mkdir -p manifests
cd manifests
mkdir -p nocap
cd nocap
```

```
nano 01-pod.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: nocap-nginx 
spec:
  containers:
    - name: web
      image: bitnami/nginx 
      securityContext:
        capabilities:
          drop:
          - all
```


```
kubectl apply -f .
kubectl get pods
kubectl logs nocap-nginx
```
