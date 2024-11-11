# Assigning Pods to Nodes


You can use any of the following methods to choose where Kubernetes schedules specific Pods:
- nodeSelector field matching against node labels
- Affinity and anti-affinity
- nodeName field
- Pod topology spread constraints
- Node labels

# Node labels
Like many other Kubernetes objects, nodes have labels. You can attach labels manually. Kubernetes also populates a standard set of labels on all nodes in a cluster.

# Node isolation/restriction
Adding labels to nodes allows you to target Pods for scheduling on specific nodes or groups of nodes. You can use this functionality to ensure that specific Pods only run on nodes with certain isolation, security, or regulatory properties.

  ## NodeRestriction
  The NodeRestriction admission plugin prevents kubelets from deleting their Node API object, and enforces kubelet modification of labels under the kubernetes.io/ or k8s.io/ prefixes as follows:
  - **Prevents** kubelets from adding/removing/updating labels with a node-restriction.kubernetes.io/ prefix. This label prefix is reserved for administrators to label their Node objects for workload isolation purposes, and kubelets will not be allowed to modify labels with that prefix.
  - **Allows** kubelets to add/remove/update these labels and label prefixes:
    - kubernetes.io/hostname
    - kubernetes.io/arch
    - kubernetes.io/os
    - beta.kubernetes.io/instance-type
    - node.kubernetes.io/instance-type
    - failure-domain.beta.kubernetes.io/region (deprecated)
    - failure-domain.beta.kubernetes.io/zone (deprecated)
    - topology.kubernetes.io/region
    - topology.kubernetes.io/zone
    - kubelet.kubernetes.io/-prefixed labels
    - node.kubernetes.io/-prefixed labels
  ##  Node isolation
  To make use of that label prefix for node isolation:
  - Ensure you are using the Node authorizer and have enabled the NodeRestriction admission plugin.
  - Add labels with the node-restriction.kubernetes.io/ prefix to your nodes, and use those labels in your node selectors. For example, example.com.node-restriction.kubernetes.io/fips=true or example.com.node-restriction.kubernetes.io/pci-dss=true
