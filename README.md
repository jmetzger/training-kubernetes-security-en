# Kubernetes Security 

## Agenda 

 1. Starting
    * [The truth about security](/kubernetes/security/truth.md)
    * [The architecture of Kubernetes](/kubernetes/architecture.md)
    * [Layers to protect (Security)](/kubernetes/security/basics/layers.md) 
    * [Kill Chain]()
   
 1. Getting hacked
    * [Why is a cluster so rewarding to hack]()
    * [Starting with Tesla](https://arstechnica.com/information-technology/2018/02/tesla-cloud-resources-are-hacked-to-run-cryptocurrency-mining-malware/)

 1. Category 1 by Layer: OS / Kernel
    * [Securing the OS and the Kernel](kubernetes-/security/01-os-kernel/hardening-os-kernel.md)
    * [Kernel Hardening Checker](kernel/hardening.md)
   
 1. Category 2 by Layer: Cluster
    * [Securing the components]()
    * [Least Privileges with RBAC]()
    * [AdmissionController - What for ? ]()
    * [AdmissionController - How they work ?]()
   
 1. Category 3 by Layer: Pods Container

    * [Great but still alpha User Namespaces]()
    
 1. Category 4 by Layer: Application 

 1. Development

 1. Build

 1. Deployment

 1. Production 

 1. Prevention 

 1. Detection / Monitoring 
    * [Vulnerability Scanning]()
    * [Runtime Scanning - Falco] 
    * [Should I use security tools ?]
    * [Which should I use ? How to find out if abandoned ?]

 1. Reaction 
    * [The Audits Logs](kubernetes/security/reaction/auditing.md)

   

 1. Grundlagen
    * [Workloads-Phasen und Absicherung](grundlagen/workloads-phasen-und-absicherung.md)
    * Die sicherheitsrelevanten Ebenen in Kubernetes
    * Typische Angriffsvektoren 

 1. Nodes 
    * Absichern der Nodes
    * Härten und die Angriffsoberfläche verringern 

 1. RBAC
    * Wie funktioniert RBAC ?
    * An welchen Stelle spielt RBAC in Kubenetes eine Rolle ?
    * Komponenten / Objekte von RBAC
    * Praktische Umsetzung von RBAC

 1. Sicherheitsregeln durchsetzen
    * Admission Controller
    * PSA (PodSecurity Adminssion)
    * Übung mit dem PSA
   
 1. Pod Sicherheit
    * ServiceAccounts (automount) mounten oder nicht?
    * Muss jeder Pod auf den Kuberentes Api - Server zugreifen können?
    * Sicherheitskritische Themen in Bezug auf Pods

 1. Unprivilegierte Pods/Container
    * Was ist zu beachten?
    * Welche Images setze ich ein?
    * Wie kann ich Probleme lösen?
    * Wie debugge ich non-root - Container/Pods?
    * Praktische Verwendung eins non-root pod

 1. Der Security Context
    * Was ist der SecurityContext?
    * seccomp
    * Linux capabilities
    * privileged/unprivileged
    * appArmor / SELinux
     
 1. Network Policies
    * Network Policies verstehen
    * Network Policies praktisch umsetzen

 1. ServiceMesh
    * Warum ein ServiceMesh ?
    * Funktionsweise eines ServiceMeshs?
    * Verwendung eines ServiceMeshs anhand von istio

 1. Image Security
    * Image Security Scanning


## Backlog 

  1. Kubernetes - Überblick
     * [Aufbau Allgemein](/kubernetes/architecture.md)
     * [Structure Kubernetes Deep Dive](https://github.com/jmetzger/training-kubernetes-advanced/assets/1933318/1ca0d174-f354-43b2-81cc-67af8498b56c)
     * [Ports und Protokolle](https://kubernetes.io/docs/reference/networking/ports-and-protocols/)
     * [kubelet garbage collection](kubelet-garbage-collection.md)

  1. Kubernetes Controlplane
     * [Renew Certificate](kubernetes-controlplane/renew-certs.md)
     * [HA-Cluster](kubernetes-controlplane/ha-cluster.md)
  
  1. Installation 
     * [Kubernetes mit der Cluster API aufsetzen](clusterapi/installation.md)
     * [Kubernetes mit kubadm aufsetzen (calico)](kubeadm/installation-cni-calico.md)

  1. Kubernetes Praxis API-Objekte 
     * [Das Tool kubectl (Devs/Ops) - Spickzettel](/kubectl/spickzettel.md)
     * [Bauen einer Applikation mit Resource Objekten](bauen-einer-webanwendung.md)
     * [kubectl/manifest/deployments](/kubectl-examples/03-nginx-deployment.md)
     * [Services - Aufbau](/kubernetes/services-aufbau.md)
     * [kubectl/manifest/service](/kubectl-examples/03b-service.md)
     * [DNS - Resolution - Services](kubernetes-networks/dns-resolution-services.md)
     * DaemonSets (Devs/Ops)
     * [Hintergrund Ingress](/kubernetes/ingress.md) 
     * [Beispiel mit Hostnamen](/kubectl-examples/04-ingress-nginx-with-hostnames.md)
     * [Configmap MariaDB - Example](kubectl-examples/06a-configmap-mariadb.md)
    
  1. Kubernetes - Probes
     * [Überblick Probes](probes/overview.md) 
  
  1. Kubernetes - Wartung / Debugging 
     * [Netzwerkverbindung zu pod testen](/tipps-tricks/verbindung-zu-pod-testen.md)

  1. Kubernetes Backup 
     * [Backups mit Velero](/backups/cluster-backup-velero.md)

  1. Kubernetes Upgrade 
     * [Upgrade von tanzu (Cluster API)](upgrade/vmware-vsphere-tanzu-tkg.md)
  
  1. Monitoring with Prometheus / Grafana 
     * [Overview](prometheus/overview.md)
     * [Setup prometheus/Grafana with helm](prometheus/walkthrough-installation-setup.md)
     * [exporters mongodb](prometheus/exporters-and-mongodb.md)
     * [Good Kubernetes Board for Grafana](prometheus/grafana/good-board.md)
     
  1. Kubernetes Tipps & Tricks 
     * [kubectl kubeconfig mergen](/kubectl/merge-kubeconfig.md)

  1. Kubernetes Certificates (Control Plane) / Security
     * [vmware - cluster api](https://docs.vmware.com/en/VMware-Tanzu-Kubernetes-Grid/1.6/vmware-tanzu-kubernetes-grid-16/GUID-cluster-lifecycle-secrets.html)
     * [Pod Security Admission (PSA)](/kubernetes-security/pod-security-admission.md)
     * [Pod Security Policy (PSP)](/kubernetes-security/pod-security-policy.md)

  1. Kubernetes Network / Firewall 
     * [Calico/Cilium - nginx example NetworkPolicy](/kubernetes-network/callico/00-simple-example.md)
     * [Egress / Ingress Examples with Exercise](/kubernetes-networks/examples-ingress-egress.md)
     * [Mesh / istio](sammlung-istio.md) 

  1. Kubernetes Probes (Liveness and Readiness) 
     * [Übung Liveness-Probe](/probes/uebung-liveness.md)
     * [Übung Liveness http aus nginx](/probes/exercise-liveness-http-nginx.md)
     * [Funktionsweise Readiness-Probe vs. Liveness-Probe](/probes/readiness.md) 
     * [Manueller Check readyz endpoint kubernetes api server aus pod](/probes/readyz-kube-api-curl.md)

  1. Kubernetes QoS / Limits / Requests
     * [Quality of Service - evict pods](kubernetes/qos-class.md)
     * [Tools to identify LimitRange and Requests](kubernetes/tools-identify-limits-request.md)

  1. Kubernetes Autoscaling 
     * [Autoscaling Pods/Deployments](/kubernetes/autoscaling.md)

  1. Kubernetes Deployment Scenarios 
     * [Deployment green/blue,canary,rolling update](/kubernetes/deployment-strategies-en.md)
     * [Service Blue/Green](/kubectl-examples/03c-service-blue-green-nginx.md)
     * [Praxis-Übung A/B Deployment](/kubectl-examples/08-ab-deployment.md)
    
  1. Kubernetes Istio
     * [Istio vs. Ingress Überblick](istio/00-istio-vs-ingress.md)
     * [Istio installieren und Addons bereitsstellen](istio/01-install-and-addons.md)
     * [Istion Überblick - egress und ingress - gateway](/istio/02-overview-ingress-egress-gateway.md)
     * [Istio - Deployment of simple application](istio/03-deploy-first-app.md)
     * [Istio - Grafana Dashboard](istio/04-grafana-dashboard.md)

## Backlog 

  1. Kubernetes - Misc 
     * [Wann wird podIP vergeben ?](kubectl/run-with-example.md)
     * [Bash completion installieren](kubectl/bash-completion.md)
     * [Remote-Verbindung zu Kubernetes (microk8s) einrichten](microk8s/connect-from-remote.md)
     * [vim support for yaml](vim/vim-yaml.md)     

  1. Kubernetes - Netzwerk (CNI's) / Mesh
     * [Netzwerk Interna](/kubernetes-networks/networking-internal-overview.md)
     * [Übersicht Netzwerke](/kubernetes-networks/overview.md) 
     * [IPV4/IPV6 Dualstack](https://kubernetes.io/docs/concepts/services-networking/dual-stack/)
     * [Ingress controller in microk8s aktivieren](microk8s/ingress.md) 

  1. Kubernetes - Ingress 
     * [ingress mit ssl absichern](/kubernetes-security/ingress-ssl.md)

  1. Kubernetes - Wartung / Debugging 
     * [kubectl drain/uncordon](/kubectl/uncordon-drain.md)
     * [Alte manifeste konvertieren mit convert plugin](/kubectl/convert-plugin.md)
     * [Curl from pod api-server](/kubernetes-advanced/curl-api-server.md)

  1. Kubernetes Praxis API-Objekte
     * [kubectl example with run](/kubectl/run-with-example.md)
     * [Ingress Controller auf Digitalocean (doks) mit helm installieren](/digitalocean/ingress-auf-digitalocean-mit-helm.md)
     * [Documentation for default ingress nginx](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/)
     * [Beispiel Ingress](/kubectl-examples/04-ingress-nginx.md)
     * [Install Ingress On Digitalocean DOKS](/digitalocean/install-ingress-helm.md)
     * [Achtung: Ingress mit Helm - annotations](/ingress-mit-helm-class-achtung.md)
     * [Permanente Weiterleitung mit Ingress](/kubectl-examples/05-ingress-permanent-redirect.md)
     * [ConfigMap Example](/kubectl-examples/06-configmap.md)
     * [Configmap MariaDB my.cnf](kubectl-examples/06b-mariadb-configmap-configfile.md)     
     
  1. Helm (Kubernetes Paketmanager) 
     * [Helm Grundlagen](/helm/grundlagen.md)
     * [Helm Warum ?](/helm/warum.md)
     * [Helm Example](/helm/example.md)

  1. Kubernetes - RBAC 
     * [Nutzer einrichten microk8s ab kubernetes 1.25](/kubernetes/rbac-create-user-kubernetes-1-25.md)
     * [Tipps&Tricks zu Deploymnent - Rollout](/kubectl/rollout.md) 

  1. Kustomize 
     * [Kustomize Overlay Beispiel](/kustomize/02-overlay-example.md)
     * [Helm mit kustomize verheiraten](/kustomize/helm-kustomize-options.md)

  1. Kubernetes - Tipps & Tricks 
     * [Kubernetes Debuggen ClusterIP/PodIP](/tipps-tricks/cluster-ip-debug.md)
     * [Debugging pods](tipps-tricks/debugging-pods.md)
     * [Taints und Tolerations](kubernetes/taints-tolerations.md)
     * [pod aus deployment bei config - Änderung neu ausrollen](https://github.com/stakater/Reloader)

  1. Kubernetes Advanced 
     * [Curl api-server kubernetes aus pod heraus](kubernetes-advanced/curl-api-server.md)

  1. Kubernetes - Documentation 
     * [Documentation zu microk8s plugins/addons](https://microk8s.io/docs/addons)  
     * [Shared Volumes - Welche gibt es ?](https://kubernetes.io/docs/concepts/storage/volumes/)

  1. Kubernetes - Hardening 
     * [Kubernetes Tipps Hardening](kubernetes-security/tipps-hardening.md)
     * [Kubernetes Security Admission Controller Example](kubernetes-security/pod-security-admission.md)
     * [Was muss ich bei der Netzwerk-Sicherheit beachten ?](kubernetes-security/network-tasks-security-overview.md)
     
  1. Kubernetes Interna / Misc.
     * [OCI,Container,Images Standards](docker-alternatives-kubernetes.md)
     * [Geolocation Kubernetes Cluster](https://learnk8s.io/bite-sized/connecting-multiple-kubernetes-clusters)

  1. Kubernetes - Überblick
     * [Installation - Welche Komponenten from scratch](/kubernetes/installation-components-overview.md)

  1. Kubernetes - microk8s (Installation und Management) 
     * [kubectl unter windows - Remote-Verbindung zu Kuberenets (microk8s) einrichten](kubectl-windows.md)
     * [Arbeiten mit der Registry](microk8s/registry.md)
     * [Installation Kubernetes Dashboard](/microk8s/dashboard.md) 

  1. Kubernetes - RBAC 
     * [Nutzer einrichten - kubernetes bis 1.24](/kubernetes/rbac-create-user.md) 
     
  1. kubectl 
     * [Tipps&Tricks zu Deploymnent - Rollout](/kubectl/rollout.md) 
     
  1. Kubernetes - Monitoring (microk8s und vanilla) 
     * [metrics-server aktivieren (microk8s und vanilla)](/microk8s/metrics-server.md)

  1. Kubernetes - Backups 
     + [Kubernetes Aware Cloud Backup - kasten.io](/backups/cluster-backup-kasten-io.md)

  1. Kubernetes - Tipps & Tricks 
     * [Assigning Pods to Nodes](/tipps-tricks/pods-2-nodes.md) 

  1. Kubernetes - Documentation 
     * [LDAP-Anbindung](https://github.com/apprenda-kismatic/kubernetes-ldap)
     * [Helpful to learn - Kubernetes](https://kubernetes.io/docs/tasks/)
     * [Environment to learn](https://killercoda.com/killer-shell-cks)
     * [Environment to learn II](https://killercoda.com/)
     * [Youtube Channel](https://www.youtube.com/watch?v=01qcYSck1c4)

  1. Kubernetes - Shared Volumes 
     * [Shared Volumes with nfs](shared-volumes/nfs-multi.md)

  1. Kubernetes - Hardening 
     * [Kubernetes Tipps Hardening](kubernetes-security/tipps-hardening.md)


       

     

