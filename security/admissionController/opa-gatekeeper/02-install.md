# OPA Gatekeeper - Walkthrough 

## Step 1: Installation (helm) 

```
helm repo add gatekeeper https://open-policy-agent.github.io/gatekeeper/charts

cd
mkdir -p manifests 
cd manifests 
mkdir gatekeeper
cd gatekeeper
```


```
nano values.yaml
```

```
# we need this for a later exercise
enableExternalData: true
```


```
helm upgrade gatekeeper/gatekeeper --install --name-template=gatekeeper --namespace gatekeeper-system --create-namespace -f values.yaml
```

## Step 2: Webhooks (lookaround)

  * This create a mutation and a validationWebhook

```
kubectl get validatingwebhookconfigurations gatekeeper-validating-webhook-configuration 
kubectl get mutatingwebhookconfigurations gatekeeper-mutating-webhook-configuration 


```

  * Let's look in the mutation more deeply 

```
kubectl get mutationgwebhookconfigurations gatekeeper-mutatiing-webhook-configuration -o yaml
```

## Step 3: The components 

```
# controllers are the endpoint for the webhooking
# audit is done every 60 seconds in the audit-pod 
kubectl -n gatekeeper-system get all
```
     
