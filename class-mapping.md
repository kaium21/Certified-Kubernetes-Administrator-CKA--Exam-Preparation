**Table of Contents:**
- [1. Class Mapping and Task](#1-class-mapping-and-task)
  - [1.1. Class1 : Install Kubernetes Cluster](#11-class1--install-kubernetes-cluster)
  - [1.2. Class2: Install Cilium CNI](#12-class2-install-cilium-cni)
  - [1.3. Class3 :  YAML, Kubernetes Object and Resources](#13-class3---yaml-kubernetes-object-and-resources)
  - [1.4. Class4 : Kubernetes Object, Resources and Local Path Provisioner](#14-class4--kubernetes-object-resources-and-local-path-provisioner)
  - [1.5. Class: Troubleshooting](#15-class-troubleshooting)
- [2. References](#2-references)


# 1. Class Mapping and Task


## 1.1. Class1 : Install Kubernetes Cluster

- [Install Kubernetes Cluster](./install/lab-setup/v1.31/README.md)
- [Visit CNCF Landscape ](https://landscape.cncf.io/)


## 1.2. Class2: Install Cilium CNI 

- [Troubleshoot Kubernetes Cluster - Installation Procedure, Kubelet]
- [Install Cilium CNI](./install/cilium/README.md)


## 1.3. Class3 :  YAML, Kubernetes Object and Resources

- [YAML](./docs/yaml-tutorial/README.md)
- Exploring [Kubernetes Cluster Information/Componets](https://kubernetes.io/docs/concepts/architecture/)
- [Exploring Kubectl command](https://kubernetes.io/docs/reference/kubectl/) and It's config file
- [Explore kubeconfig file](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/)
- [Finding Information from a Certificate File](https://www.baeldung.com/linux/openssl-extract-certificate-info)
- Provision [a sample nginx Webserver](./docs/07-kubernetes-applications/first-simple-application/README.md) and expose service to outside of world
- Explore [Label concept](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) and apply filter using a label
- Use of [`kubectl description` command](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_describe/)
- Talk about [imperative command](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/imperative-command/)
- View [kubectl](https://kubernetes.io/docs/reference/kubectl/) output as human readable, yaml and json format
- [Troubleshoot - swap space](./docs/04-troubleshoot/RAEDME.md)
- For deep understanding of Kubernetes Cluster Installation and Componets explore [Kubernetes Hardway, this is not part this course scope, but investing time on it will give immense power of Kubernetes World](https://github.com/kelseyhightower/kubernetes-the-hard-way)


Ref:
- https://kubernetes.io/docs/concepts/architecture/
- https://kubernetes.io/docs/reference/kubectl/
- https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/
- https://kubernetes.io/docs/tasks/manage-kubernetes-objects/imperative-command/
- https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/
- https://kubernetes.io/docs/reference/kubectl/generated/kubectl_describe/
- https://github.com/kelseyhightower/kubernetes-the-hard-way
- https://www.baeldung.com/linux/openssl-extract-certificate-info




## 1.4. Class4 : Kubernetes Object, Resources and Local Path Provisioner

- [Use of crictl](https://kubernetes.io/docs/tasks/debug/debug-cluster/crictl/) [*](https://github.com/kubernetes-sigs/cri-tools)
- [Install Local Path Provission, CSI](https://github.com/rancher/local-path-provisioner)








## 1.5. Class: Troubleshooting

[Follow me troubleshooting doc ](./docs/04-troubleshoot/RAEDME.md)


- [Kubelet Troubleshooting, swap space](./docs/04-troubleshoot/RAEDME.md)
- [Node Taint Issue]
- [Node label, nodeSelector]
- [Service Selector, Label Filtering]
- [Storage Issue]
- [Database Backup and Restore]




## 1.6. Class 6 : Kubernetes Object and Resources 

**Date: 28 Oct 2024**

- [access-authn-authz](https://kubernetes.io/docs/reference/access-authn-authz/authorization/)
- [Resource Request and Limit](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)
- [Namespace](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)
- [Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)
- [configure-pod-container](https://kubernetes.io/docs/tasks/configure-pod-container/)
- [Volumes](https://kubernetes.io/docs/concepts/storage/volumes/)
- [Storage](https://kubernetes.io/docs/concepts/storage/)
- [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)
- [MetalLB](https://metallb.universe.tf/installation/)
- [Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/#default-deny-all-egress-traffic)



Users in Kubernetes:
- [Create User in Kubernetes](https://aungzanbaw.medium.com/a-step-by-step-guide-to-creating-users-in-kubernetes-6a5a2cfd8c71)
- https://hbayraktar.medium.com/how-to-create-a-user-in-a-kubernetes-cluster-and-grant-access-bfeed991a0ef



```bash
kubectl auth can-i list pods --as=system:serviceaccount:default:test-sa -n default
kubectl auth can-i create pods --as=system:serviceaccount:default:test-sa -n default
```


**Home-work:**
- Create a namespae
- Create a cluster role 
- Bind cluster role a user/group/service account
- 


Ref:
- https://kubernetes.io/docs/reference/access-authn-authz/authorization/
- https://kubernetes.io/docs/reference/access-authn-authz/rbac/
- https://kubernetes.io/docs/reference/access-authn-authz/rbac/#kubectl-create-role
- https://kubernetes.io/docs/reference/kubectl/generated/kubectl_auth/kubectl_auth_whoami/
- https://kubernetes.io/docs/reference/kubectl/generated/kubectl_auth/kubectl_auth_can-i/
- https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
- https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
- https://kubernetes.io/docs/tasks/configure-pod-container/
- https://kubernetes.io/docs/concepts/storage/
- https://kubernetes.io/docs/concepts/storage/volumes/
- https://kubernetes.io/docs/concepts/storage/persistent-volumes/
- https://kubernetes.io/docs/concepts/services-networking/ingress/
- https://metallb.universe.tf/installation/
- https://github.com/arif332/kubernetes-tutorial/blob/main/installation/k3d-k3s/k3d-metallb-nginx-ingress-integration.md
- https://kubernetes.io/docs/concepts/services-networking/network-policies/#default-deny-all-egress-traffic




## 1.7. Class 7 : Review of Kubernetes Object and Resources

**Date: 4 Nov 2024**

This is a recap class with explation of following topics:
- [Draw Cluster Architecture Diagram](./docs/image/kubernetes-concept-diagram.svg)
- Explain placement of `kubectl` binary file and it's configruation
- Explain Declarative and Imperative Command
- [Explain Spec of Pod Definiton](./docs/07-kubernetes-applications/01-first-simple-application/web.yaml)
- [Explain Spec and Template of Deployment config](./docs/07-kubernetes-applications/04-deployment-ssl-mount/README.md)
- [Explain Mount and VolumentMounts for SSL Secret](./docs/07-kubernetes-applications/04-deployment-ssl-mount/README.md)
- [Explain vim editing, help can be taken from here](https://arif332.github.io/blog/kubernetes/certification/security/cloud%20native/2021/08/02/kubernetes-cks-exam-certification-tips.html)



Will explain in next class:
- [Resource Quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/)



Ingress, Pod, Deployment: 

![Relation of Ingress, Pod & Deployment](./docs/image/client-ingress-service-pod.png)



Ref:
- https://kubernetes.io/docs/concepts/policy/resource-quotas/




## 1.8. Class 8 : Review Kubernetes Object and Resources with More Example

**Date: 7 Nov 2024**

- [Exaplain the communication flow in sequence diagram](https://tetrate.io/blog/kubernetes-networking/)
- [Operator](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/)
- [Assigning Pods to Nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)
- [DNS for Services and Pods](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)
- [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)
- [Ingress Installation](https://kubernetes.github.io/ingress-nginx/deploy/#quick-start)
- [Metrics Server Installation](https://github.com/kubernetes-sigs/metrics-server)
- [Taint and Toleration Example]()
- [Autoscaling, Horizontal & Vertical scaling]()
- [Liveness, readiness and startup probe Example]()
- [Add limits to a pod/deployment Example]()


[Example of nodeSelector](./docs/07-kubernetes-applications/09-nodeselector-exmaple/README.md)


Ref:
- https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/
- https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector


**Metrics Server:**
[Follow me to install Metrics Server](./install/metrics-server/README.md)


**kube-dns:**
```bash

```

Ref:
https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/#dns-search-domain-list-limits


**Ingrss-controller:**
[Follow me to install ingress-nginx controller](./install/ingress-controller/README.md)


**Metal-lb:**
[Follow me to install metal-lb](./install/metal-lb/README.md)


Add/remove taint on a node:
```bash
k taint node dc78def55f1c.mylabserver.com node-role.kubernetes.io/control-plane:NoSchedule-
k taint node dc78def55f1c.mylabserver.com node-role.kubernetes.io/control-plane:NoSchedule
```

Ref:
- https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/



Quota:


Ref:
- https://kubernetes.io/docs/concepts/policy/resource-quotas/





**Task:**
- Install Ingress
- Install MetalLB and define IPPool for LoadBalancer IP Address
- Install Metrics Server
- Practice scale, autoscale
- Practice taint/tolleration with nodeSelector
- Explore Metrics
- Explore CustomResource
- Lable and LabelSelector
- Change Node Label
- Service Namming Concept interms of namespace and cluster



Ref:
- https://tetrate.io/blog/kubernetes-networking/
- https://github.com/containernetworking/cni/blob/main/SPEC.md#section-2-execution-protocol
- https://kubernetes.io/docs/concepts/extend-kubernetes/operator/
- https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/
- https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/
- https://kubernetes.io/docs/concepts/services-networking/ingress/
- https://kubernetes.io/docs/concepts/services-networking/ingress/#tls
- https://kubernetes.github.io/ingress-nginx/
- https://github.com/kubernetes-sigs/metrics-server
- https://metallb.universe.tf/installation/#installation-by-manifest
- https://metallb.universe.tf/configuration/








## 1.9. Networking

- [Network Policy](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
- [Ingress Controllers](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/)
- [Create Ingress Resource]()
- 

Ref:
- https://kubernetes.io/docs/concepts/cluster-administration/networking/
- https://kubernetes.io/docs/concepts/services-networking/network-policies/
- https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/
- https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/


## 1.10. Storage

- [Storage](https://kubernetes.io/docs/concepts/storage/)
- [Install Local Path Provission, CSI](https://github.com/rancher/local-path-provisioner)
- [Create PV]
- [Create PVC]


Ref:
- https://kubernetes.io/docs/concepts/storage/
- https://github.com/rancher/local-path-provisioner
- 



## 1.11. Application Package Manager – Helm & Customize

- [Install Helm](https://helm.sh/docs/intro/quickstart/)
- [Kustomize](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/)


Ref:
- https://helm.sh/docs/intro/quickstart
- https://github.com/kubernetes-sigs/kustomize
- https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/





## 1.12. Kubernetes Platform Maintenance

- [ETCD Note](./docs/05-system-maintenance/etcd-backup-restore/README.md)
- [ETCD Backup](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#built-in-snapshot)
- [Restoring an etcd cluster](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#restoring-an-etcd-cluster)


Ref:
- https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/
- https://etcd.io/docs/v3.5/op-guide/maintenance/




## 1.13. Kubernetes Platform Lifecycle Management

- [Kubernetes Cluster Software upgrade](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)


Ref:
- https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/

## 1.14. Container and Kubernetes Security




## 1.15. Class: Troubleshooting

[Follow me troubleshooting doc ](./docs/04-troubleshoot/RAEDME.md)


- [Kubelet Troubleshooting, swap space](./docs/04-troubleshoot/RAEDME.md)
- [Node Taint Issue]
- [Node label, nodeSelector]
- [Service Selector, Label Filtering]
- [Storage Issue]
- [Database Backup and Restore]



## 1.16. Exam Bootcamp for CKA Exam

- Here will explain question scenario. 
- Exam tips




## 1.17. Applications

Ref:
- https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/
- https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/
- [Run Applications](https://kubernetes.io/docs/tasks/run-application/)

 


## 1.18. Others

- [Control plane deployment options](https://kubernetes.io/docs/concepts/architecture/#control-plane-deployment-options)


# 2. References
- https://kubernetes.io/docs/home/
