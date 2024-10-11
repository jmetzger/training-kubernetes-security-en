# Securing kubelet 

## Breach 1: bypass adminission controller 

```
If a static Pod fails admission control, the kubelet won't register the
Pod with the API server. However, the Pod still runs on the node. 
```

  * https://kubernetes.io/docs/concepts/security/api-server-bypass-risks/


### Mitigate breach: Disable the directory for static pods on worker-nodes 

  * https://kubernetes.io/docs/concepts/security/api-server-bypass-risks/#static-pods-mitigations

```
# change the setting kubelef-config
staticPodPath: /etc/kubernetes/manifests
# -> to
staticPodPath: 
```

```
after that:
```
![image](https://github.com/user-attachments/assets/34b1ac5d-1d27-4785-b5eb-e2db24b90476)

https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-reconfigure/


  * Only Enable the behaviour really needed
  * https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/#static-pod-creation
    
## Breach 2: Allowing anonymous access to kubelet 


### Disabling it in anycase 

  * in the newer of kubeadm it is already the case
  * Check with provider / installer 

```
 authentication:
      anonymous:
        enabled: false

```
![image](https://github.com/user-attachments/assets/34b1ac5d-1d27-4785-b5eb-e2db24b90476)
