# Mounting the serviceAccount 

```
a. Delete your token 
kubectl delete secret training-token 
```

```
# only if it was not there yet 
kubectl create sa training
kubectl create rolebinding training-binding --clusterrole=cluster-admin --systemaccount=default:training
```

```
cd
mkdir  -p manifests 
cd manifests 
mkdir sa-podtest 
cd sa-podtest
kubectl run kubectltester2 --image=alpine --overrides='{ "spec": { "serviceAccount": "training" }  }' --dry-run=client -o yaml > 01-pod.yaml 
cat 01-pod.yaml 

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: kubectltester2
  name: kubectltester2
spec:
  containers:
  - image: alpine
    command:
      - sleep
      - infinity
    name: kubectltester2
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  serviceAccount: training
status: {}



# exec into pod -> container 
kubectl exec -it kubectltester2 -- sh 
# token 


# jwt.io 
# get the output
```
