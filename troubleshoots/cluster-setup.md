# Problem 01 : when run the any kubectl command in worker node
```  kubectl get nodes ```

## Showing Output:
```text
E1020 16:38:01.393464    7502 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"http://localhost:8080/api?timeout=32s\": dial tcp 127.0.0.1:8080: connect: connection refused"
E1020 16:38:01.395054    7502 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"http://localhost:8080/api?timeout=32s\": dial tcp 127.0.0.1:8080: connect: connection refused"
E1020 16:38:01.396613    7502 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"http://localhost:8080/api?timeout=32s\": dial tcp 127.0.0.1:8080: connect: connection refused"
E1020 16:38:01.398399    7502 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"http://localhost:8080/api?timeout=32s\": dial tcp 127.0.0.1:8080: connect: connection refused"
E1020 16:38:01.400399    7502 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"http://localhost:8080/api?timeout=32s\": dial tcp 127.0.0.1:8080: connect: connection refused"
The connection to the server localhost:8080 was refused - did you specify the right host or port?
```

## Solution:

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/kubelet.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl get nodes
```

### Output
```text
NAME          STATUS   ROLES           AGE   VERSION
controlnode   Ready    control-plane   6d    v1.31.1
workernode1   Ready    <none>          6d    v1.31.1
workernode2   Ready    <none>          23h   v1.31.1
```


