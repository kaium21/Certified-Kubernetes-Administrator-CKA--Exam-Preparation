When run the `kubeadm init` command, showing the below error.
Error:
```
[init] Using Kubernetes version: v1.31.2
[preflight] Running pre-flight checks
error execution phase preflight: [preflight] Some fatal errors occurred:
        [ERROR NumCPU]: the number of available CPUs 1 is less than the required 2
        [ERROR Mem]: the system RAM (1000 MB) is less than the minimum 1700 MB
[preflight] If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
To see the stack trace of this error execute with --v=5 or higher

```
Solution:
1. Please go through the minimum requirement to install kubeadm
# Check:
- One or more machines running a deb/rpm-compatible Linux OS; for example: Ubuntu or CentOS.
- 2 GiB or more of RAM per machine--any less leaves little room for your apps.
- At least 2 CPUs on the machine that you use as a control-plane node.
- Full network connectivity among all machines in the cluster. You can use either a public or a private network

[Reference](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)

3. When run
```
W1031 17:33:59.421715    1632 version.go:109] could not fetch a Kubernetes version from the internet: unable to get URL "https://dl.k8s.io/release/stable-1.txt": Get "https://dl.k8s.io/release/stable-1.txt": context deadline exceeded (Client.Timeout exceeded while awaiting headers)
W1031 17:33:59.421932    1632 version.go:110] falling back to the local client version: v1.31.2
[init] Using Kubernetes version: v1.31.2
[preflight] Running pre-flight checks
        [WARNING Swap]: swap is supported for cgroup v2 only. The kubelet must be properly configured to use swap. Please refer to https://kubernetes.io/docs/concepts/architecture/nodes/#swap-memory, or disable swap on the node
[preflight] Pulling images required for setting up a Kubernetes cluster
[preflight] This might take a minute or two, depending on the speed of your internet connection
[preflight] You can also perform this action beforehand using 'kubeadm config images pull'
```
4. After upgrdating
```
kubeadm init
W1031 17:33:59.421715    1632 version.go:109] could not fetch a Kubernetes version from the internet: unable to get URL "https://dl.k8s.io/release/stable-1.txt": Get "https://dl.k8s.io/release/stable-1.txt": context deadline exceeded (Client.Timeout exceeded while awaiting headers)
W1031 17:33:59.421932    1632 version.go:110] falling back to the local client version: v1.31.2
[init] Using Kubernetes version: v1.31.2
[preflight] Running pre-flight checks
        [WARNING Swap]: swap is supported for cgroup v2 only. The kubelet must be properly configured to use swap. Please refer to https://kubernetes.io/docs/concepts/architecture/nodes/#swap-memory, or disable swap on the node
[preflight] Pulling images required for setting up a Kubernetes cluster
[preflight] This might take a minute or two, depending on the speed of your internet connection
[preflight] You can also perform this action beforehand using 'kubeadm config images pull'


[certs] Using certificateDir folder "/etc/kubernetes/pki"
[certs] Generating "ca" certificate and key
[certs] Generating "apiserver" certificate and key
[certs] apiserver serving cert is signed for DNS names [controlnodegp kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local] and IPs [10.96.0.1 192.168.175.21]
[certs] Generating "apiserver-kubelet-client" certificate and key
[certs] Generating "front-proxy-ca" certificate and key
[certs] Generating "front-proxy-client" certificate and key
[certs] Generating "etcd/ca" certificate and key
[certs] Generating "etcd/server" certificate and key
[certs] etcd/server serving cert is signed for DNS names [controlnodegp localhost] and IPs [192.168.175.21 127.0.0.1 ::1]
[certs] Generating "etcd/peer" certificate and key
[certs] etcd/peer serving cert is signed for DNS names [controlnodegp localhost] and IPs [192.168.175.21 127.0.0.1 ::1]
[certs] Generating "etcd/healthcheck-client" certificate and key
[certs] Generating "apiserver-etcd-client" certificate and key
[certs] Generating "sa" key and public key
[kubeconfig] Using kubeconfig folder "/etc/kubernetes"
[kubeconfig] Writing "admin.conf" kubeconfig file
[kubeconfig] Writing "super-admin.conf" kubeconfig file
[kubeconfig] Writing "kubelet.conf" kubeconfig file
[kubeconfig] Writing "controller-manager.conf" kubeconfig file
[kubeconfig] Writing "scheduler.conf" kubeconfig file
[etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
[control-plane] Using manifest folder "/etc/kubernetes/manifests"
[control-plane] Creating static Pod manifest for "kube-apiserver"
[control-plane] Creating static Pod manifest for "kube-controller-manager"
[control-plane] Creating static Pod manifest for "kube-scheduler"
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Starting the kubelet
[wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests"
[kubelet-check] Waiting for a healthy kubelet at http://127.0.0.1:10248/healthz. This can take up to 4m0s

[kubelet-check] The kubelet is not healthy after 4m0.000429063s

Unfortunately, an error has occurred:
        The HTTP call equal to 'curl -sSL http://127.0.0.1:10248/healthz' returned error: Get "http://127.0.0.1:10248/healthz": context deadline exceeded


This error is likely caused by:
        - The kubelet is not running
        - The kubelet is unhealthy due to a misconfiguration of the node in some way (required cgroups disabled)

If you are on a systemd-powered system, you can try to troubleshoot the error with the following commands:
        - 'systemctl status kubelet'
        - 'journalctl -xeu kubelet'

Additionally, a control plane component may have crashed or exited when started by the container runtime.
To troubleshoot, list all containers using your preferred container runtimes CLI.
Here is one example how you may list all running Kubernetes containers by using crictl:
        - 'crictl --runtime-endpoint unix:///var/run/crio/crio.sock ps -a | grep kube | grep -v pause'
        Once you have found the failing container, you can inspect its logs with:
        - 'crictl --runtime-endpoint unix:///var/run/crio/crio.sock logs CONTAINERID'
error execution phase wait-control-plane: could not initialize a Kubernetes cluster
To see the stack trace of this error execute with --v=5 or higher
```

-
Check Kubelet Status: Run the following commands to see the status and logs for kubelet:

```
 systemctl status kubelet
● kubelet.service - kubelet: The Kubernetes Node Agent
     Loaded: loaded (/lib/systemd/system/kubelet.service; enabled; vendor preset: enabled)
    Drop-In: /usr/lib/systemd/system/kubelet.service.d
             └─10-kubeadm.conf
     Active: activating (auto-restart) (Result: exit-code) since Thu 2024-10-31 17:54:49 UTC; 9s ago
       Docs: https://kubernetes.io/docs/
    Process: 10615 ExecStart=/usr/bin/kubelet $KUBELET_KUBECONFIG_ARGS $KUBELET_CONFIG_ARGS $KUBELET_KUBEADM_ARGS $KUBELET_EXTRA_AR>
   Main PID: 10615 (code=exited, status=1/FAILURE)
        CPU: 52ms
lines 1-9/9 (END)
```
```
systemctl status kubelet
● kubelet.service - kubelet: The Kubernetes Node Agent
     Loaded: loaded (/lib/systemd/system/kubelet.service; enabled; vendor preset: enabled)
    Drop-In: /usr/lib/systemd/system/kubelet.service.d
             └─10-kubeadm.conf
     Active: activating (auto-restart) (Result: exit-code) since Thu 2024-10-31 17:54:49 UTC; 9s ago
       Docs: https://kubernetes.io/docs/
    Process: 10615 ExecStart=/usr/bin/kubelet $KUBELET_KUBECONFIG_ARGS $KUBELET_CONFIG_ARGS $KUBELET_KUBEADM_ARGS $KUBELET_EXTRA_AR>
   Main PID: 10615 (code=exited, status=1/FAILURE)
        CPU: 52ms
lines 1-9/9 (END)
^C
root@controlnodegp:~# journalctl -xeu kubelet
░░ Defined-By: systemd
░░ Support: http://www.ubuntu.com/support
░░
░░ Automatic restarting of the unit kubelet.service has been scheduled, as the result for
░░ the configured Restart= setting for the unit.
Oct 31 17:56:00 controlnodegp systemd[1]: Stopped kubelet: The Kubernetes Node Agent.
░░ Subject: A stop job for unit kubelet.service has finished
░░ Defined-By: systemd
░░ Support: http://www.ubuntu.com/support
░░
░░ A stop job for unit kubelet.service has finished.
░░
░░ The job identifier is 14222 and the job result is done.
Oct 31 17:56:00 controlnodegp systemd[1]: Started kubelet: The Kubernetes Node Agent.
░░ Subject: A start job for unit kubelet.service has finished successfully
░░ Defined-By: systemd
░░ Support: http://www.ubuntu.com/support
░░
░░ A start job for unit kubelet.service has finished successfully.
░░
░░ The job identifier is 14222.
Oct 31 17:56:00 controlnodegp kubelet[11105]: Flag --container-runtime-endpoint has been deprecated, This parameter should be set v>
Oct 31 17:56:00 controlnodegp kubelet[11105]: Flag --pod-infra-container-image has been deprecated, will be removed in a future rel>
Oct 31 17:56:00 controlnodegp kubelet[11105]: I1031 17:56:00.848680   11105 server.go:211] "--pod-infra-container-image will not be>
Oct 31 17:56:00 controlnodegp kubelet[11105]: I1031 17:56:00.853722   11105 server.go:491] "Kubelet version" kubeletVersion="v1.31.>
Oct 31 17:56:00 controlnodegp kubelet[11105]: I1031 17:56:00.853766   11105 server.go:493] "Golang settings" GOGC="" GOMAXPROCS="" >
Oct 31 17:56:00 controlnodegp kubelet[11105]: I1031 17:56:00.854052   11105 server.go:934] "Client rotation is on, will bootstrap i>
Oct 31 17:56:00 controlnodegp kubelet[11105]: I1031 17:56:00.856068   11105 certificate_store.go:130] Loading cert/key pair from "/>
Oct 31 17:56:00 controlnodegp kubelet[11105]: I1031 17:56:00.858836   11105 dynamic_cafile_content.go:160] "Starting controller" na>
Oct 31 17:56:00 controlnodegp kubelet[11105]: I1031 17:56:00.865217   11105 server.go:1431] "Using cgroup driver setting received f>

```

Cgroups Configuration: Kubelet may be misconfigured due to issues with cgroups. Make sure Kubernetes is configured to use systemd for cgroup management. This is often done by updating the kubelet configuration file:


Start CRI-O:
```
systemctl start crio.service
```

Disable swap space:
# make swap off, for permant change /etc/fstab
swapoff -a

# Change network config:
```
modprobe br_netfilter
sysctl -w net.ipv4.ip_forward=1
```
# Or, to change network setting permanently:
```
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.ipv4.ip_forward = 1
EOF
sudo sysctl --system
sysctl net.ipv4.ip_forward
```

```
 kubeadm init
W1031 18:02:23.676648   13557 version.go:109] could not fetch a Kubernetes version from the internet: unable to get URL "https://dl.k8s.io/release/stable-1.txt": Get "https://dl.k8s.io/release/stable-1.txt": context deadline exceeded (Client.Timeout exceeded while awaiting headers)
W1031 18:02:23.676754   13557 version.go:110] falling back to the local client version: v1.31.2
[init] Using Kubernetes version: v1.31.2
[preflight] Running pre-flight checks
error execution phase preflight: [preflight] Some fatal errors occurred:
        [ERROR Port-6443]: Port 6443 is in use
        [ERROR Port-10259]: Port 10259 is in use
        [ERROR Port-10257]: Port 10257 is in use
        [ERROR FileAvailable--etc-kubernetes-manifests-kube-apiserver.yaml]: /etc/kubernetes/manifests/kube-apiserver.yaml already exists
        [ERROR FileAvailable--etc-kubernetes-manifests-kube-controller-manager.yaml]: /etc/kubernetes/manifests/kube-controller-manager.yaml already exists
        [ERROR FileAvailable--etc-kubernetes-manifests-kube-scheduler.yaml]: /etc/kubernetes/manifests/kube-scheduler.yaml already exists
        [ERROR FileAvailable--etc-kubernetes-manifests-etcd.yaml]: /etc/kubernetes/manifests/etcd.yaml already exists
        [ERROR Port-10250]: Port 10250 is in use
        [ERROR Port-2379]: Port 2379 is in use
        [ERROR Port-2380]: Port 2380 is in use
        [ERROR DirAvailable--var-lib-etcd]: /var/lib/etcd is not empty
[preflight] If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
To see the stack trace of this error execute with --v=5 or higher
```




The errors indicate that there’s an existing Kubernetes installation or leftover resources from a previous setup attempt. Here's how to clean up and start fresh:
- Stop Kubernetes Services: Stop any running Kubernetes services, including kubelet, to free up ports.
```
sudo systemctl stop kubelet
```
- Remove Existing Kubernetes Files and Directories:
Remove Kubernetes manifest files:
```
sudo rm -rf /etc/kubernetes/manifests
```
Remove the etcd data directory:
```
sudo rm -rf /var/lib/etcd
```

Clear any other related Kubernetes directories:
```
sudo rm -rf /etc/kubernetes
```

- Free Up Ports: Check which processes are using the conflicting ports (6443, 10259, 10257, 10250, 2379, and 2380) and stop them if necessary:
```
sudo lsof -i :6443 -i :10259 -i :10257 -i :10250 -i :2379 -i :2380
```

output:
```
COMMAND     PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
kube-apis 12066 root    3u  IPv6  36887      0t0  TCP *:6443 (LISTEN)
kube-apis 12066 root   72u  IPv6  37232      0t0  TCP ip6-localhost:33432->ip6-localhost:6443 (ESTABLISHED)
kube-apis 12066 root   74u  IPv6  37234      0t0  TCP ip6-localhost:6443->ip6-localhost:33432 (ESTABLISHED)
```

Stop any process using these ports or kill them directly:
```
sudo kill -9 12066
```

# Reset kubeadm: Use kubeadm reset to clear out any previous Kubernetes setup:
```
sudo kubeadm reset -f
```
Output:
```
sudo kubeadm reset -f
[preflight] Running pre-flight checks
W1031 18:34:12.542241   25040 removeetcdmember.go:106] [reset] No kubeadm config, using etcd pod spec to get data directory
[reset] Deleted contents of the etcd data directory: /var/lib/etcd
[reset] Stopping the kubelet service
[reset] Unmounting mounted directories in "/var/lib/kubelet"
[reset] Deleting contents of directories: [/etc/kubernetes/manifests /var/lib/kubelet /etc/kubernetes/pki]
[reset] Deleting files: [/etc/kubernetes/admin.conf /etc/kubernetes/super-admin.conf /etc/kubernetes/kubelet.conf /etc/kubernetes/bootstrap-kubelet.conf /etc/kubernetes/controller-manager.conf /etc/kubernetes/scheduler.conf]

The reset process does not clean CNI configuration. To do so, you must remove /etc/cni/net.d

The reset process does not reset or clean up iptables rules or IPVS tables.
If you wish to reset iptables, you must do so manually by using the "iptables" command.

If your cluster was setup to utilize IPVS, run ipvsadm --clear (or similar)
to reset your system's IPVS tables.

The reset process does not clean your kubeconfig files and you must remove them manually.
Please, check the contents of the $HOME/.kube/config file.
```

# Remove CNI Configuration:

```
sudo rm -rf /etc/cni/net.d
```

# Check for Remaining CNI Plugins (optional): If you’re using a specific CNI plugin (like Calico or Flannel), you may also need to remove the corresponding CNI binaries. These are typically located in /opt/cni/bin.

```
sudo rm -rf /opt/cni/bin/*
```

# Reinitialize kubeadm: Once the CNI configuration is removed, you can re-run kubeadm init to initialize the cluster.
```
sudo kubeadm init
```

# Output:

```
W1031 18:53:17.384342   31811 version.go:109] could not fetch a Kubernetes version from the internet: unable to get URL "https://dl.k8s.io/release/stable-1.txt": Get "https://dl.k8s.io/release/stable-1.txt": context deadline exceeded (Client.Timeout exceeded while awaiting headers)
W1031 18:53:17.384446   31811 version.go:110] falling back to the local client version: v1.31.2
[init] Using Kubernetes version: v1.31.2
[preflight] Running pre-flight checks
[preflight] Pulling images required for setting up a Kubernetes cluster
[preflight] This might take a minute or two, depending on the speed of your internet connection
[preflight] You can also perform this action beforehand using 'kubeadm config images pull'
[certs] Using certificateDir folder "/etc/kubernetes/pki"
[certs] Generating "ca" certificate and key
[certs] Generating "apiserver" certificate and key
[certs] apiserver serving cert is signed for DNS names [controlnodegp kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local] and IPs [10.96.0.1 192.168.175.21]
[certs] Generating "apiserver-kubelet-client" certificate and key
[certs] Generating "front-proxy-ca" certificate and key
[certs] Generating "front-proxy-client" certificate and key
[certs] Generating "etcd/ca" certificate and key
[certs] Generating "etcd/server" certificate and key
[certs] etcd/server serving cert is signed for DNS names [controlnodegp localhost] and IPs [192.168.175.21 127.0.0.1 ::1]
[certs] Generating "etcd/peer" certificate and key
[certs] etcd/peer serving cert is signed for DNS names [controlnodegp localhost] and IPs [192.168.175.21 127.0.0.1 ::1]
[certs] Generating "etcd/healthcheck-client" certificate and key
[certs] Generating "apiserver-etcd-client" certificate and key
[certs] Generating "sa" key and public key
[kubeconfig] Using kubeconfig folder "/etc/kubernetes"
[kubeconfig] Writing "admin.conf" kubeconfig file
[kubeconfig] Writing "super-admin.conf" kubeconfig file
[kubeconfig] Writing "kubelet.conf" kubeconfig file
[kubeconfig] Writing "controller-manager.conf" kubeconfig file
[kubeconfig] Writing "scheduler.conf" kubeconfig file
[etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
[control-plane] Using manifest folder "/etc/kubernetes/manifests"
[control-plane] Creating static Pod manifest for "kube-apiserver"
[control-plane] Creating static Pod manifest for "kube-controller-manager"
[control-plane] Creating static Pod manifest for "kube-scheduler"
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Starting the kubelet
[wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests"
[kubelet-check] Waiting for a healthy kubelet at http://127.0.0.1:10248/healthz. This can take up to 4m0s
[kubelet-check] The kubelet is healthy after 501.284883ms
[api-check] Waiting for a healthy API server. This can take up to 4m0s
[api-check] The API server is healthy after 3.501501783s
[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config" in namespace kube-system with the configuration for the kubelets in the cluster
[upload-certs] Skipping phase. Please see --upload-certs
[mark-control-plane] Marking the node controlnodegp as control-plane by adding the labels: [node-role.kubernetes.io/control-plane node.kubernetes.io/exclude-from-external-load-balancers]
[mark-control-plane] Marking the node controlnodegp as control-plane by adding the taints [node-role.kubernetes.io/control-plane:NoSchedule]
[bootstrap-token] Using token: 9fqwfv.sjkmdvfny6tc6qlh
[bootstrap-token] Configuring bootstrap tokens, cluster-info ConfigMap, RBAC Roles
[bootstrap-token] Configured RBAC rules to allow Node Bootstrap tokens to get nodes
[bootstrap-token] Configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstrap-token] Configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstrap-token] Configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[bootstrap-token] Creating the "cluster-info" ConfigMap in the "kube-public" namespace
[kubelet-finalize] Updating "/etc/kubernetes/kubelet.conf" to point to a rotatable kubelet client certificate and key
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.175.21:6443 --token 9fqwfv.sjkmdvfny6tc6qlh \
        --discovery-token-ca-cert-hash sha256:201879ef75281311821dff46ed064419f2d631c61246b5c9623a3ee0002b92f2
```
# For checking purpose for non-root user:

## To start using your cluster, you need to run the following as a regular user:
```
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

## For Root User:
Alternatively, if you are the root user, you can run:
```
  export KUBECONFIG=/etc/kubernetes/admin.conf
```

kubectl get nodes
NAME            STATUS   ROLES           AGE     VERSION
controlnodegp   Ready    control-plane   5m49s   v1.31.2
