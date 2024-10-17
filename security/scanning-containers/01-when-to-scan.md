# Image Scanning - When ? 

## When to scan ?

  * In Development
  * When Building Software (before pushing to the registry)
  * Before Deploying Software
  * In Production
  * Ongoing in the registry itself 

## Conceptional Ideas 

  1. Scan the image when built before being pushed
  1. In Kubernetes Cluster only images from your corporate private registry
     and k8s.io 
     (Option: Only allow signed images, where signing is verified)  
  1. (Policy) To always pull when starting a new Deployment,Pod,Statefulset (private repo)  

## Why ? 

  * We want to be sure, our system is not compromised
  * One way of compromising is an malicious image, that we use
  * We want to avoid this.

## Which approach do we take here....

  * For our own images, that we build, we want to be sure, they are all "clean" before being pushed to the registry


