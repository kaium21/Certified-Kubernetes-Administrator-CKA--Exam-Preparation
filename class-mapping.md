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





# 2. References
- https://kubernetes.io/docs/home/


