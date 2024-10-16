# Do not mount if not needed

## Why ?

  * Every attacker tries to get as much information as possible
  * Although there are not severe permissions in here, show as little information as possible
  * For example, use will see, which namespace he is in ;o)

## Disable ?

```
# enabled by default 
kubectl explain pod.spec.automountServiceToken
```
