# EnableServiceLinks 

## What ? 

  * This show other services in the network in the enviroment variables  -> env in the pod

## Disable it: Why ? 

  * If your pod is compromised, that is one of the first places the attacker will look int
    * to find out, which other services in the namespaces are next to you
   
## Howto ? 

```
...
kind: Pod
spec:
  enableServiceLinks: false
...
```

```
kubectl explain pod.spec.enableServiceLinks
```
