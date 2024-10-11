# Is pod automounting service account / test access 

## Walkthrough 

```
kubectl run -it --rm kubectltester --image=alpine -- sh 
```

```
# in shell
apk add kubectl
# it uses in in-cluster configuration in folder
# /var/run/secrets/kubernetes.io/serviceaccount 
kubectl auth can-i --list 
```

