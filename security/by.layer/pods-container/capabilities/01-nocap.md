# Start pod without capabilities 

  * 

```
apiVersion: v1
kind: Pod
metadata:
  name: nocap
spec:
  containers:
    - name: podmagic
      image: busybox
      command: [ "sleep" ]
      args: [ "infinity" ]
      securityContext:
        capabilities:
          drop:
          - all
```
