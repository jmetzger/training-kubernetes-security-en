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

```
stages:
  - prebuild
  - build

prebuild:
  stage: prebuild
  image:
    name: docker.io/curlimages/curl:8.3.0
    entrypoint: [""]
  script:
    - curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b $CI_PROJECT_DIR v0.45.1
    - curl -L --output - https://github.com/google/go-containerregistry/releases/download/v0.16.1/go-containerregistry_Linux_x86_64.tar.gz | tar -xz crane
  artifacts:
    paths:
      - crane
      - trivy

build image:
  stage: build
  image:
    name: gcr.io/kaniko-project/executor:v1.23.2-debug
    entrypoint: [""]
  variables:
    DOCKER_IMAGE: "${CI_REGISTRY_IMAGE}:${CI_COMMIT_SHORT_SHA}"
    TRIVY_INSECURE: "true"
    TRIVY_NO_PROGRESS: "true"
  script:
    - /kaniko/executor
      --context $CI_PROJECT_DIR
      --dockerfile $CI_PROJECT_DIR/Dockerfile
      --no-push
      --tar-path image.tar
    - ./trivy image 
      --ignore-unfixed 
      --exit-code 0 
      --severity HIGH 
      --input image.tar
    - ./trivy image
      --ignore-unfixed
      --exit-code 1
      --severity CRITICAL
      --input image.tar
    - ./crane auth login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY
    - ./crane push image.tar $DOCKER_IMAGE

```



## References: 

  * https://bluelight.co/blog/how-to-set-up-trivy-scanner-in-gitlab-ci-guide
  * https://gitlab.com/bluelightco/blog-examples/trivy
  
