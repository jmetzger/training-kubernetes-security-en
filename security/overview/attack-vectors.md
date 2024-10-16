# Attack Vectors 

## What 3 types of attack vectors are there ? 

  1. External Attackers
  1. Malicious containers
  1. Compromised or malicious users 

### External Attackers 

  * You can have threat actors who have no access to the cluster but are able to reach the application running on it. 

### Malicious containers 

  * If a threat actor manages to breach a single container, they will attempt to increase their access and take over the entire cluster.

### Compromised or malicious users 

  * When you’re dealing with compromised accounts or malicious users, an attacker with stolen yet valid credentials will execute commands against network access and the Kubernetes API. 
  * Mitigation: Least Principle Policy
 
## Reference:

  * https://www.cncf.io/blog/2021/11/08/kubernetes-main-attack-vectors-tree-an-explainer-guide/

