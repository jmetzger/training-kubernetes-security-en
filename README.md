# Kubernetes Security - en

## Agenda 

  1. Starting
     * [The truth about security](/security/truth.md)
     * [The architecture of Kubernetes](/kubernetes/architecture.md)
     * [Architecture DeepDive](https://github.com/jmetzger/training-kubernetes-advanced/assets/1933318/1ca0d174-f354-43b2-81cc-67af8498b56c)
     * [Layers to protect (Security)](security/overview/layers-2-protect.md)
     * [AttackVectors](security/overview/attack-vectors.md)
     * [The route from development to production to secure](security/overview/route-2-production.md)
     * [Kill Chain](kill-chain.md)

  1. Checklist
     * [Security Checklists](/security/checklist/security-checklist.md)
   
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
     * [Overview capabilities](security/by.layer/pods-container/capabilities/00-overview.md)
     * [Start pod without capabilities & how can we see this](security/by.layer/pods-container/capabilities/01-nocap.md)
     * [Hacking and exploration session HostPID](explore/01-hack-session-hostpid.md)
     * [Disable ServiceLinksEnable false](https://github.com/jmetzger/training-kubernetes-security-en/blob/main/security/by.layer/pods-container/enableServiceLinks/disable-howto-and-why.md
) 
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

  1. Obey Security Policies (AdmissionControllers)
     * [Admission Controller](/security/admissionController/01-overview.md)
     * PSA (PodSecurity Admission)
     * [Exercise with PSA](kubernetes-security/pod-security-admission.md)
     * [OPA Gatekeeper 01-Overview](/security/admissionController/opa-gatekeeper/01-overview.md)
     * [OPA Gatekeeper 02-Install with Helm](/security/admissionController/opa-gatekeeper/02-install.md)
     * [OPA Gatekeeper 03-Simple Exercise](/security/admissionController/opa-gatekeeper/05-example-exercise.md)
     * [OPA Gatekeeper 04-Example-Job-Debug](/security/admissionController/opa-gatekeeper/06-example-job-debug.md)
     * [Connaisseur: Verifying images before Deployment](/security/admissionController/connaisseur-image-verification/02-walkthrough.md)
   
  1. Pod Security
     * [Automount ServiceAccounts or not ?](security/by.layer/pods-container/serviceAccount/do-not-mount-if-not-needed.md)
     * Does every pod need to access the kubenernetes api server?
   
  1. Unprivilegierte Pods/Container
     * [Which images to use ?](security/unprivileged-containers/which-images.md) 
     * How can i debug non-root - Container/Pods?
    
  1. The SecurityContext
     * seccomp
     * privileged/unprivileged
     * [appArmor example](https://kubernetes.io/docs/tutorials/security/apparmor/)
     * SELinux
     
  1. Network Policies
     * Understand NetworkPolicies
     * [Exercise NetworkPolicies](kubernetes-networkpolicy/00-simple-exercises-group-en.md)
     * [CNI Benchmarks](https://itnext.io/benchmark-results-of-kubernetes-network-plugins-cni-over-40gbit-s-network-2024-156f085a5e4e)

  1. ServiceMesh
     * [Why a ServiceMesh ?](istio/overview/benefits-of-a-service-mesh.md)
     * [How does a ServiceMeshs work? (example istio](/istio/overview/overview-classic-sidecar.md)
     * [istio security features](istio/overview/security-features.md)
     * [istio-service mesh - ambient mode](/istio/overview/ambient-mode.md)
     * [Performance comparison - baseline,sidecar,ambient](/istio/overview/performance-comparison-baseline-sidecar-ambient.md)
     
  1. Image Security
     * [When to scan ?](security/scanning-containers/01-when-to-scan.md)
     * [Example Image Security Scanning - using gitlab and trivy](security/scanning-containers/02-example-trivy-gitlab.md)

  1. Hacking Sessions
     * [Hacking with HostPID](/explore/01-hack-session-hostpid.md)

  1. Documentation
     * [Great video about attacking kubernetes - older, but some stuff is still applicable](https://www.youtube.com/watch?v=HmoVSmTIOxM)
     * [Straight forward hacking session of kubernetes](https://youtu.be/iD_klswHJQs?si=97rWNuAbGjLwCjpa)
     * [github with manifests for creating bad pods](https://bishopfox.com/blog/kubernetes-pod-privilege-escalation#pod8)
