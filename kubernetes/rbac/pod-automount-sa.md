# Is pod automounting service account / test access 

## Walkthrough 

```
cd
mkdir -p manifests
cd manifests
mkdir podsa
cd podsa
```

```
kubectl run -it --rm kubectltester --image=bitnami/kubectl -- sh 
```

