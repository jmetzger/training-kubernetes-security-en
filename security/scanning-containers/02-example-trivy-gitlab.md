# Example Image Scanning with Gitlab and Trivy

## Pre-Thoughts 

 * Gitlab offers a security scanner based on Trivy
 * BUT: This scanner tests already uploading images
 * If we think about ShiftLeft-appraoch (Security early) on, this might not be the best approach

## What needs to be done ?

  1. We want to scan directly after building the image, but before pushing
  1. If we have vulnerabilities with HIGH-Score (CVE), the pipeline will fail (and it stops)
     * Image is not uploaded 


