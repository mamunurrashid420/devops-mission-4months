# Ubuntu Network Configuration Guide

This README provides step-by-step commands to check network settings, configure hostnames, and set a static IP on Ubuntu systems using Netplan.

# Ubuntu Network Configuration Guide

This guide documents basic network diagnostic commands, hostname management, and static IP configuration using **Netplan** on Ubuntu.

---

## 1. Network Checks

### IP Configuration
```bash
ipconfig
```

### Routing Table
```bash
route -n
```

### DNS Configuration
```bash
cat /etc/resolv.conf
```

### Physical Connectivity
```bash
ip link
```

---

## 2. Hostname Configuration

### Show Current Hostname
```bash
hostname
```

### Set a New Hostname
```bash
sudo hostnamectl set-hostname <hostname>
```

### Verify Hostname
```bash
hostnamectl status
```

---

## 3. Static IP Configuration (Netplan)

Edit the Netplan configuration file:
```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

Example configuration:
```yaml
# This is the network config written by 'subiquity'
network:
  ethernets:
    enp0s3:
      dhcp4: false
      addresses: [10.10.120.11/24]
      gateway4: 10.10.120.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
  version: 2
```

Apply the configuration:
```bash
sudo netplan apply
```

---

## Notes
- Replace `enp0s3` with your actual network interface name (find it with `ip link`).
- Verify your static IP assignment after applying:
  ```bash
  ip addr
  ```