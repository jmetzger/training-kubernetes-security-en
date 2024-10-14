# MutationAdmissionWebhook And ValidateAdmissionWebhook 

## What are they for ? 

  * Enhance your Admissions on runtime by using these Hooks

## What do the mutationAdmissionWebHook's do ? 

  * Execute before the validating Webhooks
  * Calls a service/pod that does a mutation (changes the object, e.g. pod, new fields, annotations a.s.o)
  * The object is passed to the pod as json. 
  * This is defined with the following object: 

```
mutatingwebhookconfigurations
```

![image](https://github.com/user-attachments/assets/f3029e47-86b8-40e2-8360-4b05d4e956d4)

  * You can find out if there are any configured, by looking for these:

```
kubectl get mutatingwebhookconfigurations
```

## What do the validatingAdmissionWebhook's do ?

  * Execute after the mutation Webhooks
  * Call a service/pod that will do validation (The pod is completely free what to validate)
  * The object is passed to the pod for validation
  * This is defined with the following object:

```
validatingwebhookconfigurations 
``` 

```
# Here you can find out, if any are configured
kubectl get validatingwebhookconfigurations
```
