# Open Policy Agent (OPA Gatekeeper) 

## How does it work ?

  * It is called by the definition in mutationAdmissionWebhook and validatingAdmissionWebhook

## What can the OPA Gatekeeper do ? 

  * It can validate
  * It can mutate

## How does it do this ?

  * It uses a language which is called REGO
  * It uses objects like

```
apiVersion: templates.gatekeeper.sh/v1
kind: ConstraintTemplate

apiVersion: templates.gatekeeper.sh/v1
kind: Constraint
```

  * for the validation 
