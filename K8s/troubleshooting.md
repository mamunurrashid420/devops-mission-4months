## If you facing this type of issue
```bash
## kubectl get pods
E1009 04:00:44.672608    1301 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://10.1.0.4:6443/api?timeout=32s\": dial tcp 10.
E1009 04:00:44.673913    1301 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://10.1.0.4:6443/api?timeout=32s\": dial tcp 10.
E1009 04:00:44.675214    1301 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://10.1.0.4:6443/api?timeout=32s\": dial tcp 10.
E1009 04:00:44.676512    1301 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://10.1.0.4:6443/api?timeout=32s\": dial tcp 10.
E1009 04:00:44.677812    1301 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://10.1.0.4:6443/api?timeout=32s\": dial tcp 10.
The connection to the server 10.1.0.4:6443 was refused - did you specify the right host or port?
```
checking this issue 
- Run on the master node:
    ```
    ps -ef | grep kube-apiserver

    ```
- Check Kubelet status:

    ```
    systemctl status kubelet
    ```
- Verify Docker/Containerd service status:
    ```
    systemctl status docker
    ```
- Check network connectivity:
    ```
    ping 10.1.0.4
    ```
- Check firewall rules:
    ```
    sudo ufw status
    ```
- Check SELinux status:
    ```
    sudo getenforce
    ```
- If its stopped
    ```
    systemctl restart containerd
    # or 
    systemctl restart docker
    ```

- Now check 
    ```
    kubectl get pods
    # or 
    kubectl get nodes
    ```
- Output 
- `kubect get pods -A`
    ## ✅ Kubernetes System Pods Status

    Below is the current status of all system pods running in the cluster:

    ```bash
    NAMESPACE         NAME                                       READY   STATUS    RESTARTS        AGE
    kube-system       calico-kube-controllers-689744956f-f6t9l   1/1     Running   1 (2m22s ago)   16h
    kube-system       calico-node-bkhkm                          1/1     Running   1 (7m33s ago)   16h
    kube-system       calico-node-dzb59                          1/1     Running   1 (2m22s ago)   16h
    kube-system       calico-node-m5v5q                          1/1     Running   0               65s
    kube-system       coredns-668d6bf9bc-gxpxl                   1/1     Running   1 (2m22s ago)   16h
    kube-system       coredns-668d6bf9bc-npmgp                   1/1     Running   1 (2m22s ago)   16h
    kube-system       etcd-master                                1/1     Running   1 (2m22s ago)   16h
    kube-system       kube-apiserver-master                      1/1     Running   1 (2m22s ago)   16h
    kube-system       kube-controller-manager-master             1/1     Running   1 (2m22s ago)   16h
    kube-system       kube-proxy-4vfcn                           1/1     Running   1 (57s ago)     65s
    kube-system       kube-proxy-nkv8k                           1/1     Running   1 (7m33s ago)   16h
    kube-system       kube-proxy-wc5ls                           1/1     Running   1 (2m22s ago)   16h
    kube-system       kube-scheduler-master                      1/1     Running   1 (2m22s ago)   16h
    tigera-operator   tigera-operator-789496d6f5-gsqr2           1/1     Running   1 (2m22s ago)   16h


## Liveness, Readiness, and Startup Probes
1. Livenes probe


## kubectl patch 
kubectl patch command is used to modify the configuration of an existing Kubernetes resource (such as a Pod, Deployment, or Service) `without applying the entire YAML file again`.

The meaning of `kubectl patch` is - 
*instead of changing the entire configuration, it updates only a small part of it.*

If i am updating replicas in deployment yaml file. like 3 to 5 
```
kubectl patch deployment myapp-deployment -p '{"spec":{"replicas":5}}'
```