# Verifying images before using them in Deployment (admissionController)

## Prerequisites

  * You must have create a private/public key pair
  * You must have signed some images in your registry on docker Hub.
  * This was done here: [Signing an image with cosign](/security/signing-images/01-signing.md)
    

## Step 1: Install Connaissuer with helm 

```
cd
mkdir -p manifests
cd manifests
mkdir connaisseur
cd connaisseur
```

```
nano values.yaml
```

```
# 1. We will add the public key of ours in validators: cosign->type:cosign 
# 2. We will add a policy for the system to know, when to use it:
  - pattern: "docker.io/dockertrainereu/*:*"
      validator: cosign
# Unfortunately we muss add everything from the defaults values file
# concerning -> validators, policy
# I have tested this .... 
```

```
application:
  features:
      namespacedValidation:
            mode: validate

# validator options: https://sse-secure-systems.github.io/connaisseur/latest/validators/
  validators:
    - name: allow
      type: static
      approve: true
    - name: deny
      type: static
      approve: false
    - name: cosign
      type: cosign
      trustRoots:
        - name: default
          key: |
            -----BEGIN PUBLIC KEY-----
            MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAE2LmRkI8sNi6fSluqU5UEisptlwZl
            YaJBAJqTf96ccM4R3MstL8PfR5fhy877TG7bnpc4YnlfejT6F7XE71FWkA==
            -----END PUBLIC KEY-----
    - name: dockerhub
      type: notaryv1
      trustRoots:
        - name: default # root from dockerhub
          key: |
            -----BEGIN PUBLIC KEY-----
            MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEOXYta5TgdCwXTCnLU09W5T4M4r9f
            QQrqJuADP6U7g5r9ICgPSmZuRHP/1AYUfOQW3baveKsT969EfELKj1lfCA==
            -----END PUBLIC KEY-----
        - name: sse # root from sse
          key: |
            -----BEGIN PUBLIC KEY-----
            MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEsx28WV7BsQfnHF1kZmpdCTTLJaWe
            d0CA+JOi8H4REuBaWSZ5zPDe468WuOJ6f71E7WFg3CVEVYHuoZt2UYbN/Q==
            -----END PUBLIC KEY-----

  policy:
    - pattern: "*:*"
      validator: deny
    - pattern: "docker.io/dockertrainereu/*:*"
      validator: cosign
    - pattern: "docker.io/library/*:*"
      validator: dockerhub
    - pattern: "docker.io/securesystemsengineering/*:*"
      validator: dockerhub
      with:
        trustRoot: sse
    - pattern: "registry.k8s.io/*:*"
      validator: allow
```

```
# Add the repo
helm repo add connaisseur https://sse-secure-systems.github.io/connaisseur/charts
# Install the helm chart
helm upgrade connaisseur connaisseur/connaisseur --install --create-namespace --namespace connaisseur -f values.yaml
```

## Step 2: Create a namespace and label it with connaisseur 

  * In our example we apply it only in a specific namespace
  * But you can also use it for all namespaces
  * According to: https://sse-secure-systems.github.io/connaisseur/latest/features/namespaced_validation/

```
# create namespace
kubectl create ns app1
kubectl label ns app1 securesystemsengineering.connaisseur/webhook=validate
```

## Step 3: Try to run image in namespace 

```
# image from docker -> works 
kubectl -n app1 run nginxme --image=nginx:1.23

# signed image from dockertrainereu 
kubectl -n app1 run pod1 --image=dockertrainereu/alpine-rootless:1.20

# unsigned image from dockertrainereu
kubectl -n app1 run pod1 --image=dockertrainereu/pinger
```
