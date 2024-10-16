# What security features does istio offer ? 

## Pod-2-Pod Encryption (mtls)

  * mtls (mutual tls)

## Authorization Policies 

  * How is allowed to connect to which service

```
apiVersion: security.istio.io/v1
kind: AuthorizationPolicy
metadata:
  name: foo
spec:
  action: ALLOW
  rules:
  - to:
    - operation:
        paths: ["/public"]
```
