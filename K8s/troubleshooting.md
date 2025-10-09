## If you facing this type of issue
```
 kubectl get pods
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

