# runAs 

  * Best practices. Set on level of the pod
  * The it also reflects containers that are started with kubectl debug (ephemerla containers)

## runAsUser 

  * Important: UID does not need to exist in container 
  * Really run as specific user.
  * If not set the user from Dockerfile is taken
  * Recommended to set it here, that will be deep defense line
    * If image has a root user or can not run as root this will fail 

## runAsGroup 

  * Recommended to set this as well 

## runAsNonRoot 

  * Indicates that use must run as none root
  * If this is not configure in the image, the start fails
