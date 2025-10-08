## How to Configure Kubernetes Cluster on Ubuntu 22.04 (Azure vm)
### Azure VM Network Configuration & Kubernetes Node Connectivity Report
- Azure VM Network Configuration 
    - Step 1: Create a Virtual Network (VNet)
        - Go to Virtual Networks in the Azure portal.
        - Click on "Create virtual network".
            - Name: `k8s-vnet`
            - Region: East US
            - Address space: 172.16.0.0/16
            - subnet name: `k8s-subnet`
            - subnet address range: 172.16.100.0/24
    - Step 4: Create a Virtual Machine (VM)
        - Create Two or more VMS.
            - `Master Node `: k8s-master
            - `Worker Node`: k8s-worker-1
            - `Worker Node`: k8s-worker-2
            - `Worker Node`: k8s-worker-3
        - During VM Creation, under Networking 
            - Same Virtual Network(vNet):  `k8s-vnet`
            - Same subnet: `k8s-subnet`

1. Setting up Static IPV4 on all nodes (Master & Worker Node)
`sudo vim /etc/netplan/01-network-manager-all.yaml`

```
network:
  ethernets:
    enp0s3:
      dhcp4: false
      addresses: [172.16.100.14/24]
      gateway4: 172.16.100.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
  version: 2
  ```
  - apply `sudo netplan apply`

2.1.  Update all nodes
`sudo apt update`

2.2. Disable swap on all nodes
`sudo swapoff -a`

2.3. Disable swap on startup
`sudo vim /etc/fstab`

2.4. reboot all nodes
`sudo init 6`

3. Installing Kubernetes components on all nodes (Master & Worker Node).

3.1. Configure modules (Master & Worker Node).
```
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF
```
- Load modules (Master & Worker Node)
`sudo modprobe overlay`
`sudo modprobe br_netfilter`

3.2 Configure Networking (Master & Worker Node)
configure sysctl (Master & Worker Node)
```
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF
```
- Apply new settings (Master & Worker Node)
`sudo sysctl --system`

3.3. Install containerd (Master & Worker Node)
```
sudo apt-get update && sudo apt-get install -y containerd
containerd config default | sudo tee /etc/containerd/config.toml >/dev/null 2>&1
sudo sed -i 's/            SystemdCgroup = false/            SystemdCgroup = true/g' /etc/containerd/config.toml
sudo systemctl restart containerd
sudo systemctl enable containerd
```

3.5 Install Kubernetes Management Tools (Master & Worker Node).
```
sudo apt-get update
sudo apt-get install -y ca-certificates curl
sudo apt-get install -y apt-transport-https ca-certificates curl


curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.32/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg

echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.32/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
```
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```
4. Initialization the Kubernetes Cluster (Master Node).
```
kubeadm init 
```
5. Configuring Kubectl (Master Node).
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
6. Install Calico networking for on-premises deployments (Master Node)
```
curl https://raw.githubusercontent.com/projectcalico/calico/v3.26.1/manifests/calico.yaml -O
kubectl apply -f calico.yaml
```
7. Print Join token for worker Node to join Cluster (Master Node).
```
kubeadm token create --print-join-command
```

- Now check running pods and service
```
kubectl get pods -A
kubectl get svc -A
```
Congratulations! You have successfully configured a Kubernetes cluster on Ubuntu 22.04.
