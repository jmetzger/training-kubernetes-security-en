# Workloads - Phasen und Absicherung 

## Phase 1: Build - Phase / Bau - Phase 

### Was passiert hier ? 

  * Sofware wird gebaut für Deine Workload (Applikation)
  * Infrastruktur-Komponenten und Host-Komponenten (bare metal oder virtuelle Maschinen)
    * werden bereitgestellt.

 ### Wo liegt hier das Sicherheits-Augenmerk

   * Sicherheit der CI/CD Pipeline
   * Sicherheit für die Image-Repos implementieren.(Best practices)
     * Kompromittierung der Images muss sichergestellt werden
     * Wer hat überhaupt Zugriff auf die Repos ?
   * Passwörter und Sicherheitsschlüssel "sicher" verwalten
     (vs. Secrets in Kubernetes)
   * Host - Betriebssystem absichern.
   * Sicherscans der verwendeten Images    

## Phase 2: Deployment 

### Was passiert hier ? 

  * Kubernetes Platform aufsetzen, um Applikation deployen zu können

 ### Wo liegt hier das Sicherheitsaugenmerk ?

  * Cluster härten
  * Firewalls
  * Sicherheits - (Nutzer) - Gruppen 
  * Admission Controllers
  * Services bereitstellen 

## Phase 3: Runtime / Betrieb 

### Was passiert hier ? 

### Wo liegt hier das Sicherheitsausgenmerk ?

   * Network Policy
   * Application Layer Policy
   * Observability
   * Encryption
   * Auditing
   * Threat Detection 
