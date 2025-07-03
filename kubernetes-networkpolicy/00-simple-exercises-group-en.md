# Simple Network Policy Example (for group in 1 cluster)

## Step 1: Create Deployment and Service 

```
SHORT=jm
kubectl create ns policy-demo-$SHORT 
```

```
cd 
mkdir -p manifests
cd manifests
mkdir -p np
cd np
```

```
nano 01-deployment.yml
```

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 1
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.23
        ports:
        - containerPort: 80
```

```
kubectl -n policy-demo-$SHORT apply -f . 
```

```
nano 02-service.yml
```

```
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  type: ClusterIP # Default Wert 
  ports:
  - port: 80
    protocol: TCP
  selector:
    app: nginx
```

```
kubectl -n policy-demo-$SHORT apply -f . 
```

## Step 2: Testing access without any rules  

```
# Run a 2nd pod to access nginx  
kubectl run --namespace=policy-demo-$SHORT access --rm -ti --image busybox
```

```
# Within the shell/after prompt
wget -q nginx -O -
exit
```

```
# Optional: Show pod in second 2. ssh-session on jump-host
kubectl -n policy-demo-$SHORT get pods --show-labels
```

## Step 3: Define policy: no access is allowed by default (in this namespace) 

```
nano 03-default-deny.yaml 
```

```
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: default-deny
spec:
  podSelector:
    matchLabels: {}
```

```
kubectl -n policy-demo-$SHORT apply -f .
```

## Step 4: Test connection with deny all rules  

```
kubectl run --namespace=policy-demo-$SHORT access --rm -ti --image busybox
```

```
# Within the shell
wget -q nginx -O -
```

## Step 5: Allow access from pods with the Label run=access (all pods startet with run with the name access do have this label by default)

```
nano 04-access-nginx.yaml 
```

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: access-nginx
spec:
  podSelector:
    matchLabels:
      app: nginx
  ingress:
    - from:
      - podSelector:
          matchLabels:
            run: access
```

```
kubectl -n policy-demo-$SHORT apply -f . 
```

## Schritt 5: Test it (access should work)

```
# Start a 2nd pod to access nginx 
# becasue of run->access pod automtically has the label run:access
kubectl run --namespace=policy-demo-$SHORT access --rm -ti --image busybox
```

```
# innerhalb der shell 
wget -q nginx -O -
```


## Step 6: start Pod with label run=no-access - this should not work 

``` 
kubectl run --namespace=policy-demo-$SHORT no-access --rm -ti --image busybox
```

```
# in der shell  
wget -q nginx -O -
```

## Step 7: Cleanup

```
kubectl delete ns policy-demo-$SHORT 
```


## Ref:

  * https://projectcalico.docs.tigera.io/security/tutorials/kubernetes-policy-basic
