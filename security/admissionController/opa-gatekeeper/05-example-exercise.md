# Example Exercise 

## Step 1: Create constraintTemplate 

  * I took this from the library: https://open-policy-agent.github.io/gatekeeper-library/website/
  * https://open-policy-agent.github.io/gatekeeper-library/website/validation/block-nodeport-services/

```
cd 
mkdir -p manifests 
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

## Step 2: Create constraint 

  * it is like an instance (in code = usage of classes, can be created multiple times)
  * the match defines, when it triggers -> when it calls the constraintTemplate for validation 

```
nano 02-constraint.yaml
```

```
apiVersion: constraints.gatekeeper.sh/v1beta1
kind: K8sBlockNodePort
metadata:
  name: block-node-port
spec:
  match:
    kinds:
      - apiGroups: [""]
        kinds: ["Service"]
```

```
kubectl apply -f . 
```

## Step 3: Test constraint with Service 

```
nano 03-service.yaml 
```

```
apiVersion: v1
kind: Service
metadata:
  name: my-service-disallowed
spec:
  type: NodePort
  ports:
    - port: 80
```

```
kubectl apply -f .
```

```
Error from server (Forbidden): error when creating "03-service.yaml":
admission webhook "validation.gatekeeper.sh" denied the request:
[block-node-port] User is not allowed to create service of type NodePort
```
