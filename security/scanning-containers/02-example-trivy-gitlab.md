# Example Image Scanning with Gitlab and Trivy

## Pre-Thoughts 

 * Gitlab offers a security scanner based on Trivy
 * BUT: This scanner tests already uploading images
 * If we think about ShiftLeft-appraoch (Security early) on, this might not be the best approach

## What needs to be done ?

  1. We want to scan directly after building the image, but before pushing
  1. If we have vulnerabilities with HIGH-Score (CVE), the pipeline will fail (and it stops)
     * Image is not uploaded 

## Trivy modes 

  * Trivy can be used standalone or as client/server
  * in our case, we will use it standalone 

## Demonstration:

  * https://gitlab.com/jmetzger/container-scanning-session


## References: 

  * https://bluelight.co/blog/how-to-set-up-trivy-scanner-in-gitlab-ci-guide
  * https://gitlab.com/bluelightco/blog-examples/trivy
  
