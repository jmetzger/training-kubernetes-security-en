# Walkthrough 

## 1. On client Dry-run to create simple manifest 

```
cd
mkdir -p manifests
cd manifests
mkdir static
cd static
```

```
kubectl run nginx --image=nginx --dry-run=client -o yaml > pod.yaml 
```

```
kubectl get nodes -o wide
# find worker1 -> ip -> INTERNAL-IP
```

## 2. On worker 1

```
# from client
ssh 11trainingdo@<worker-ip>
# pass: see chat
sudo su -
# same password
cd /etc/kubernetes/manifests
ls -la
# empty
```

```
nano pod.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

```
crictl pod
```
