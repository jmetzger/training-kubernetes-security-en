# Phase 2: Veritfy with OPA Gatekeeper 

## Step 1: Create constraint template

```
cd
mkdir -p manifests
cd manifests
mkdir verify-image-opa
cd verify-image-opa
```

```
nano 01-contraint-template.yaml
```

```
apiVersion: templates.gatekeeper.sh/v1beta1
kind: ConstraintTemplate
metadata:
  name: k8sexternaldatacosign
spec:
  crd:
    spec:
      names:
        kind: K8sExternalDataCosign
  targets:
    - target: admission.k8s.gatekeeper.sh
      rego: |
        package k8sexternaldata

        violation[{"msg": msg}] {
          # used on kind: Deployment/StatefulSet/DaemonSet
          # build a list of keys containing images
          images := [img | img = input.review.object.spec.template.spec.containers[_].image]

          # send external data request. We specifiy the provider as "cosign-gatekeeper-provider"
          response := external_data({"provider": "cosign-gatekeeper-provider", "keys": images}) 

          response_with_error(response)

          msg := sprintf("invalid response: %v", [response])
        }

        
        violation[{"msg": msg}] {
          # used on kind: Pod
          # build a list of keys containing images
          images := [img | img = input.review.object.spec.containers[_].image]

          # send external data request
          response := external_data({"provider": "cosign-gatekeeper-provider", "keys": images})

          response_with_error(response)

          msg := sprintf("invalid response: %v", [response])
        }

        response_with_error(response) {
          count(response.errors) > 0
          errs := response.errors[_]
          contains(errs[1], "_invalid")
        }

        response_with_error(response) {
          count(response.system_error) > 0
        }        
```

```
kubectl apply -f .
```
