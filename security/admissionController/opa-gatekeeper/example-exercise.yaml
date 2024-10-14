# Example Exercise 

## Step 1: Create contraintTemplate 

  * I took this from the library: https://open-policy-agent.github.io/gatekeeper-library/website/
  * https://open-policy-agent.github.io/gatekeeper-library/website/validation/block-nodeport-services/

```
cd 
mkdir manifests 
cd manifests 
mkdir restrict-node-port 
cd restrict-node-port 
```

```
nano 01-constraint-template.yaml 
```

```
apiVersion: templates.gatekeeper.sh/v1
kind: ConstraintTemplate
metadata:
  name: k8sblocknodeport
  annotations:
    metadata.gatekeeper.sh/title: "Block NodePort"
    metadata.gatekeeper.sh/version: 1.0.0
    description: >-
      Disallows all Services with type NodePort.

      https://kubernetes.io/docs/concepts/services-networking/service/#nodeport
spec:
  crd:
    spec:
      names:
        kind: K8sBlockNodePort
  targets:
    - target: admission.k8s.gatekeeper.sh
      rego: |
        package k8sblocknodeport

        violation[{"msg": msg}] {
          input.review.kind.kind == "Service"
          input.review.object.spec.type == "NodePort"
          msg := "User is not allowed to create service of type NodePort"
        }
```

```
kubectl apply -f .
```
