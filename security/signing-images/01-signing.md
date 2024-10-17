# Phase 1: Signing image

## Overview

1. We will create a private key
2. We will sign the images with that private key.

Important: We need access to the registry.

## Step 1: Preparation: Install cosign on the client. 

 * DONE BY THE TRAINER already 

```
sudo su - root 
cd /usr/src
https://github.com/sigstore/cosign/releases/download/v2.4.1/cosign_2.4.1_amd64.deb
dpkg -i cosign*
exit
```

## Step 2: create key-pair 

```
cosign generate-key-pair
```

## Step 3: signing dockertrainereu/alpine-rootless:1.20 (only by trainer) 

```
cosign sign -y --key cosign.key dockertrainereu/alpine-rootless:1.20
```

## Step 4: Verify signature 

```
cosign verify --key cosign.pub dockertrainereu/alpine-rootless:1.20
```

## Reference:

  * https://www.justinpolidori.it/posts/20220116_sign_images_with_cosign_and_verify_with_gatekeeper/
