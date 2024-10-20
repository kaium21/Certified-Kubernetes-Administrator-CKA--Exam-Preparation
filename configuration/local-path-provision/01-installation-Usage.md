# Local Path Provisioner

Reference :
- [Kubernetes 1.14: Local Persistent Volumes GA](https://kubernetes.io/blog/2019/04/04/kubernetes-1.14-local-persistent-volumes-ga/)
- [Local Persistent Volumes for Kubernetes Goes Beta](https://kubernetes.io/blog/2018/04/13/local-persistent-volumes-beta/)
- [Local Path provioing with example](https://github.com/rancher/local-path-provisioner/tree/master)

### What is a Local Persistent Volume?
A local persistent volume represents a local disk directly-attached to a single Kubernetes Node.

### What is Local Path Provisioner?
Local Path Provisioner provides a way for the Kubernetes users to utilize the local storage in each node. Based on the user configuration, the Local Path Provisioner will create either `hostPath` or `local` based persistent volume on the node automatically. It utilizes the features introduced by Kubernetes [Local Persistent Volume feature](https://kubernetes.io/blog/2018/04/13/local-persistent-volumes-beta/), but makes it a simpler solution than the built-in local volume feature in Kubernetes.


# 1 Installation
- The path for provisioning (a.k.a, store the persistent volume data) for all nodes: ```/opt/local-path-provisioner```
- Default namespace for local path provision : ```local-path-storage```
Installation:
Please use any of the method from (1.1, 1.2,1.3 or 1.4)

## 1.1 Stable:
```bash
kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/v0.0.30/deploy/local-path-storage.yaml
```
Output:
```text
namespace/local-path-storage created
serviceaccount/local-path-provisioner-service-account created
role.rbac.authorization.k8s.io/local-path-provisioner-role created
clusterrole.rbac.authorization.k8s.io/local-path-provisioner-role created
rolebinding.rbac.authorization.k8s.io/local-path-provisioner-bind created
clusterrolebinding.rbac.authorization.k8s.io/local-path-provisioner-bind created
deployment.apps/local-path-provisioner created
storageclass.storage.k8s.io/local-path created
configmap/local-path-config created
```
## Step 1.2 Development
```bash
kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml
```
## or use ```kustomize``` to deploy

## Step 1.3 stable:
```bash
kustomize build "github.com/rancher/local-path-provisioner/deploy?ref=v0.0.30" | kubectl apply -f -
```
## Step 1.4 Deployment
```bash
kustomize build "github.com/rancher/local-path-provisioner/deploy?ref=master" | kubectl apply -f -
```
# 2 After Installation

## 2.1 After installation, you should see something like the following:
Run the below command
```bash
kubectl -n local-path-storage get pod
```
Output:
```text
NAME                                     READY   STATUS    RESTARTS   AGE
local-path-provisioner-dbff48958-8jpbh   1/1     Running   0          16m
```

## 2.2 Check and follow the provisioner log using:

```bash
kubectl -n local-path-storage logs -f -l app=local-path-provisioner
```

Output like this:
```text
time="2024-10-20T18:30:28Z" level=debug msg="Applied config: {\"nodePathMap\":[{\"node\":\"DEFAULT_PATH_FOR_NON_LISTED_NODES\",\"paths\":[\"/opt/local-path-provisioner\"]}],\"storageClassConfigs\":null}"
time="2024-10-20T18:30:28Z" level=debug msg="Provisioner started"
I1020 18:30:28.709391       1 controller.go:824] "Starting provisioner controller" component="rancher.io/local-path_local-path-provisioner-dbff48958-8jpbh_6a8a9bb1-ffdc-4e3e-9951-3bf268e1d525"
I1020 18:30:28.809915       1 controller.go:873] "Started provisioner controller" component="rancher.io/local-path_local-path-provisioner-dbff48958-8jpbh_6a8a9bb1-ffdc-4e3e-9951-3bf268e1d525"
```
# 3 Usage

## 3.1 Create a `hostPath` backend Persistent Volume and a pod uses it:

```
kubectl create -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/examples/pvc/pvc.yaml
```
Output: `persistentvolumeclaim/local-path-pvc created`

```
kubectl create -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/examples/pod/pod.yaml
```
Output : `pod/volume-test created`

You should see the PV has been created:

```bash
kubectl get pv
```
Output:

```
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                 STORAGECLASS   VOLUMEATTRIBUTESCLASS   REASON   AGE
pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e   128Mi      RWO            Delete           Bound    test/local-path-pvc   local-path     <unset>                          93s
```

The PVC (Persistent Volume Claim) has been bound:

```bash
kubectl get pvc
```

Output:

```text
NAME             STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
local-path-pvc   Bound    pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e   128Mi      RWO            local-path     <unset>                 7m21s
```

And the Pod started running:

```bash
kubectl get pod
```
Output:
```text
NAME                              READY   STATUS        RESTARTS   AGE
volume-test                       1/1     Running       0          9m31s
```

Write something into the pod
```
kubectl exec volume-test -- sh -c "echo local-path-test > /data/test"
```
Then delete the pod using
```bash
kubectl delete -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/examples/pod/pod.yaml
```
Output: `pod "volume-test" deleted `

After confirm that the pod is gone, recreated the pod using
```bash
kubectl create -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/examples/pod/pod.yaml
```
Output : `pod/volume-test created`

Check the volume content:
```bash
kubectl exec volume-test -- sh -c "cat /data/test"
```
Output : `local-path-test `

Delete the pod and pvc

- Delete pod
```
kubectl delete -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/examples/pod/pod.yaml
```
Output: `pod "volume-test" deleted`

- Delete pvc
```
kubectl delete -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/examples/pvc/pvc.yaml
``` 
Output: `persistentvolumeclaim "local-path-pvc" deleted`

The volume content stored on the node will be automatically cleaned up. You can check the log of local-path-provisioner-xxx for details.
```
kubectl -n local-path-storage logs -f -l app=local-path-provisioner
```
Output:
```
I1020 18:53:51.224861       1 event.go:389] "Event occurred" object="test/local-path-pvc" fieldPath="" kind="PersistentVolumeClaim" apiVersion="v1" type="Normal" reason="Provisioning" message="External provisioner is provisioning volume for claim \"test/local-path-pvc\""
time="2024-10-20T18:54:02Z" level=info msg="Volume pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e has been created on workernode1:/opt/local-path-provisioner/pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e_test_local-path-pvc"
time="2024-10-20T18:54:02Z" level=info msg="Start of helper-pod-create-pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e logs"
time="2024-10-20T18:54:02Z" level=info msg="End of helper-pod-create-pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e logs"
I1020 18:54:02.385731       1 event.go:389] "Event occurred" object="test/local-path-pvc" fieldPath="" kind="PersistentVolumeClaim" apiVersion="v1" type="Normal" reason="ProvisioningSucceeded" message="Successfully provisioned volume pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e"
time="2024-10-20T19:10:46Z" level=info msg="Deleting volume pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e at workernode1:/opt/local-path-provisioner/pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e_test_local-path-pvc"
time="2024-10-20T19:10:46Z" level=info msg="create the helper pod helper-pod-delete-pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e into local-path-storage"
time="2024-10-20T19:10:49Z" level=info msg="Volume pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e has been deleted on workernode1:/opt/local-path-provisioner/pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e_test_local-path-pvc"
time="2024-10-20T19:10:49Z" level=info msg="Start of helper-pod-delete-pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e logs"
time="2024-10-20T19:10:49Z" level=info msg="End of helper-pod-delete-pvc-998e7c5d-6a21-42cd-b0d5-c56537e53d8e logs"
```
