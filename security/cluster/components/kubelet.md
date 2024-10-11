# Securing kubelet 

## Breach 1: bypass adminission controller 

```
If a static Pod fails admission control, the kubelet won't register the Pod with the API server. However, the Pod still runs on the node. 
```

  * https://kubernetes.io/docs/concepts/security/api-server-bypass-risks/


### Mitigate breach: Disable the directory for static pods on worker-nodes 

  * https://kubernetes.io/docs/concepts/security/api-server-bypass-risks/#static-pods-mitigations

```

```

  * Only Enable the behaviour really needed
  * https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/#static-pod-creation
    
