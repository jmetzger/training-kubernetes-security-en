# Connaisseur 

## What does it do ? 

  * Runs as ValidationAdmissionWebhook
  * Intercepts all the calls and finds out, if the call holds images to be used 
  * Verifies thes images with public keys.
  * Denies the call, if this fails

## Suppported signing solutions 

  * Notary V1 / docker trust 
  * cosign / sigstore 

## Reference 

  * https://artifacthub.io/packages/helm/connaisseur/connaisseur
  * https://sse-secure-systems.github.io/connaisseur/v3.3.1/
  * https://sysdig.com/blog/secure-kubernetes-deployment-signature-verification/
