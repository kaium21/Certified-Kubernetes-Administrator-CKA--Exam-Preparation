
Error:
```
E1031 15:14:10.582746    5128 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://192.168.0.120:6443/api?timeout=32s\": dial tcp 192.168.0.120:6443: i/o timeout"
```
Solution:
1. Go to Control Node:
```
cd /etc/kubernetes/manifests
```
2. edit kube-apiserver.yaml file with new IP
```
nano kube-apiserver.yaml
```
3. 
