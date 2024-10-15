# Testing cap new raw 

## Step 0: by trainer. create the image 

```
# Dockerfile 
FROM debian
RUN apt update -y && apt install -y iputils-ping && apt clean -y
```

## Step 1: Using dockertrainereu/pinger image 

  * debian with ping inside 

```
mkdir -p manifests
cd manifests
mkdir pingtest
cd pingtest 
```

```
nano 01-ping.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: pingtest
spec:
  containers:
    - name: podmagic
      image: dockertrainereu/pinger
      command: [ "sleep" ]
      args: [ "infinity" ]
      securityContext:
        runAsNonRoot: true
        runAsUser: 99999
        capabilities:
          drop:
          - all
```

```
kubectl apply -f 01-ping.yaml 
```

```
kubectl exec -it pingtest -- bash
```

```
ping www.google.de
cat /proc/1/status | grep -i CAP
# all zero no capabilities activated 
```


## Step 2: add cap-net-raw (in pod manifest it is NET_RAW)

  * now enable cap_net_raw (net_raw) in manifest

```
apiVersion: v1
kind: Pod
metadata:
  name: nocap
spec:
  containers:
    - name: podmagic
      image: dockertrainereu/pinger
      command: [ "sleep" ]
      args: [ "infinity" ]
      securityContext:
        runAsNonRoot: true
        runAsUser: 99999
        capabilities:
          drop:
          - all
          add:
          - NET_RAW
```


```
# delete old pod
kubectl delete -f 01-pingtest.yaml
# create pod once more
kubectl apply -f 01-pingtest.yaml 
kubectl exec -it pingtest -- bash 
```

```
# ping works
ping www.google.de
cat /proc/1/status | grep -i CAP
```

![image](https://github.com/user-attachments/assets/75ecc103-bbad-4e09-ab6f-ddecfa8e8292)

## Ref:

  * [Explanation of capabilities in the code](https://github.com/torvalds/linux/blob/master/include/uapi/linux/capability.h)
