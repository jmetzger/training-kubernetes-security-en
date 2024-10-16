# Kubernetes Security (en)

## Agenda 

 1. Starting
    * [The truth about security](/security/truth.md)
    * [The architecture of Kubernetes](/kubernetes/architecture.md)
    * [Architecture DeepDive](https://github.com/jmetzger/training-kubernetes-advanced/assets/1933318/1ca0d174-f354-43b2-81cc-67af8498b56c)
    * [Layers to protect (Security)](security/overview/layers-2-protect.md)
    * [AttackVectors](security/overview/attack-vectors.md)
    * [The route from development to production to secure](security/overview/route-2-production.md)
    * [Kill Chain](kill-chain.md)
   
 1. Getting hacked
    * [Why is a cluster so rewarding to hack](security/getting-hacked/kubernetes-rewarding.md)
    * [Starting with Tesla](https://arstechnica.com/information-technology/2018/02/tesla-cloud-resources-are-hacked-to-run-cryptocurrency-mining-malware/)

 1. Category 1 by Layer: OS / Kernel
    * [Securing the OS and the Kernel](security/os-kernel/01-harden-os-kernel.md)
    * [Kernel Hardening Checker](kernel/hardening.md)
   
 1. Category 2 by Layer: Cluster
    * [Securing the components]()
    * [Securing kubelet](security/cluster/components/kubelet.md)
    * [Least Privileges with RBAC](kubernetes/rbac/00-rbac-and-least-privileges.md)
    * [Admission Controller](/security/admissionController/01-overview.md)
   
 1. Category 3 by Layer: Pods Container
    * [The runAs Options in SecurityContext](security/by.layer/pods-container/runAs/overview.md)
    * [sysctls in pods/containers](security/by.layer/pods-container/sysctls/overview.md)
    * 
    * [Start pod without capabilities & how can we see this](security/by.layer/pods-container/capabilities/01-nocap.md)
    * [Hacking and exploration session HostPID](explore/01-hack-session-hostpid.md)
    * [Great but still alpha User Namespaces]()
    
 1. Reaction 
    * [The Audit Logs](/security/reaction/auditlog.md)

 1. RBAC
    * [How does RBAC work ?](kubernetes/rbac/01-how-does-rbac-work.md)
    * [Where does RBAC play a role ?](kubernetes/rbac/02-where-does-rbac-play-a-role.md)
    * [kubeconfig decode certificate](kubernetes/rbac/decode-local-certificate.md)
    * [kubectl check your permission - can-i](kubernetes/rbac/can-i.md)
    * [use kubectl in pod - default service account](/kubernetes/rbac/pod-automount-sa.md)
    * [create user for kubeconfig with using certificate](kubernetes/rbac/create-kubeconfig-with-cert.md)
    * Components / moving parts of RBAC
    * [practical exercise rbac](kubernetes/rbac-create-user-kubernetes-1-25.md)

 1. Obey Security Policies 
    * [Admission Controller](/security/admissionController/01-overview.md)
    * PSA (PodSecurity Admission)
    * Exercise with PSA
   
 1. Pod Security
    * Automount ServiceAccounts or not ? 
    * Does every pod need to access the kubenernetes api server?
   
 1. Unprivilegierte Pods/Container
    * Which images to use ? 
    * How can i debug non-root - Container/Pods?
    
 1. The SecurityContext
    * seccomp
    * privileged/unprivileged
    * appArmor / SELinux
     
 1. Network Policies
    * Understand NetworkPolicies
    * Exercise NetworkPolicies

 1. ServiceMesh
    * Why a ServiceMesh ?
    * How does a ServiceMeshs work?
     
 1. Image Security
    * Image Security Scanning

 1. Documentation
    * [Great video about attacking kubernetes - older, but some stuff is still applicable](https://www.youtube.com/watch?v=HmoVSmTIOxM)

