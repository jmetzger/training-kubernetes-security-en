# Aufbau 

## Schaubild 

![image](https://github.com/user-attachments/assets/751339d5-f279-483b-a9c5-1ba196c4c3b6)

## Components

### Master (Control Plane)

#### Jobs

  * The master coordinates the cluster
  * The master coordinates the activities in the cluster
    * scheduling of applications
    * to take charge of the desired state of application 
    * scaling of applications 
    * rollout of new updates

#### Components of the Master 

##### etcd

  * Persistent Storage (like a database), stores configuration and status of the cluster 
  
##### kube-controller-manager  
  
  * In charge of making sure the desired state is achieved (done trough endless loops)  
  * Communicates with the cluster through the kubernetes-api (kube-api-server)

##### kube-api-server 

  * provides api-frontend for administration (no gui)
  * Exposes an HTTP API (users, parts of the cluster and external components communicate with it)
  * REST API
 
##### kube-scheduler 

  * assigns Pods to Nodes. 
  * scheduler determines which Nodes are valid placements for each Pod in the scheduling queue 
    ( according to constraints and available resources )
  * The scheduler then ranks each valid Node and binds the Pod to a suitable Node. 
  * Reference implementation (other schedulers can be used)
 
### Nodes  

  * Nodes (Knoten) sind die Arbeiter (Maschinen), die Anwendungen ausführen
  * Ref: https://kubernetes.io/de/docs/concepts/architecture/nodes/

### Pod/Pods 

  * pods are the smallest unit you can roll out on the clustebernetes erstellt und verwaltet werden können.
  * a pod (basically another word for group) is a group of 1 or more containers
    * mutually used storage and network resources (all containers in the same pod can be reached with localhost)   
    * They are always on the same (virtual server)
    
## Control Plane Node (former: master) - components 

## Node (Minion) - components 

### General 

  * On the nodes we will rollout the applications

### kubelet

```
Node Agent that runs on every node (worker) 
its job is to download images and start containers 
```

### kube-proxy 

  * Runs on all of the nodes (DaemonSet)
  * Is in charge of setting up the network rules in iptables for the network services 
  * Kube-proxy is in charge of the network communication inside of the cluster and to the outside
  
## ref:

  * https://www.redhat.com/en/topics/containers/kubernetes-architecture
