# AdmissionController - Overview 

## What does it do ? (The picture) 

![image](https://github.com/user-attachments/assets/5f2c74ef-9557-42a0-8814-ce2b42247402)

## How do the docs describe it ? 

```
An admission controller is a piece of code that intercepts requests to the Kubernetes API server
prior to persistence of the object, but after the request is authenticated and authorized.
```

  * intercepts request = gets all the requests and validates or changes (=mutates them)
  * Reference: https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/

## What kind of admissionControllers do we have ?

   * Mutating and Validating
   * There are 2 phases of the AdmissionControlProcess: First mutating, then validating

## The static admissionPlugins 

   * There are static admissionPlugins which are activated by config
   * You can see the activated like so

```
# in our system like so.
kubectl -n kube-system describe pods kube-apiserver-controlplane  | grep enable-adm
```

```
--enable-admission-plugins=NodeRestriction
```
   * There are some that are activated by default:

```
# in Kubernetes 1.31
CertificateApproval,
CertificateSigning,
CertificateSubjectRestriction,
DefaultIngressClass,
DefaultStorageClass,
DefaultTolerationSeconds,
LimitRanger,
MutatingAdmissionWebhook,
NamespaceLifecycle,
PersistentVolumeClaimResize,
PodSecurity,
Priority,
ResourceQuota,
RuntimeClass,
ServiceAccount,
StorageObjectInUseProtection,
TaintNodesByCondition,
ValidatingAdmissionPolicy,
ValidatingAdmissionWebhook
```

  * Reference: What does which AdmissionController (= AdmissionPlugin) do ? https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#what-does-each-admission-controller-do
