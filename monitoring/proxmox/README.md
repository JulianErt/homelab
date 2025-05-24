# 🧰 Proxmox Homelab

This repository documents the setup, configuration, and purpose of all virtual machines and containers within my Proxmox-based homelab.  
It serves as a platform for self-hosting, learning, automation, and infrastructure experimentation.

---

## 🌐 Lab Overview

| ID  | Name      | Type     | OS             | Purpose                          |
|-----|-----------|----------|----------------|----------------------------------|
| 201 | domus     | LXC      | Ubuntu 22.04   | General services & sandbox       |
| 202 | servarr   | VM       | Ubuntu 22.04   | Media automation                 |

---

## 🔧 Infrastructure

- **Hypervisor:** [Proxmox VE](https://www.proxmox.com/en/proxmox-ve)
- **Storage Backend:** ZFS (local-lvm)
---

## 📦 Container / VM Configuration

[Proxmox Helper-Scripts](https://community-scripts.github.io/ProxmoxVE)

### 🏡 `DOMUS` (LXC 201)

General-purpose container for services and testing.

#### ⚙️ Specs

- **OS:** Ubuntu 22.04 LTS (LXC)
- **Type:** Unprivileged LXC
- **Cores:** 2  
- **RAM:** 4 GB  
- **Storage:** 64 GB  
- **IP:** Static via DHCP Reservation

#### 🛠️ Setup

```
pct create 201 local:vztmpl/ubuntu-22.04-standard_*.tar.gz \
  --hostname domus \
  --cores 2 \
  --memory 2048 \
  --net0 name=eth0,bridge=vmbr0,ip=dhcp \
  --rootfs local-lvm:10 \
  --unprivileged 1 \
  --features nesting=1

pct start 201

pct exec 201 -- bash -c "curl -s https://raw.githubusercontent.com/<your-username>/homelab/main/config/domus-init.sh | bash"
```

### 🧩 `servarr` (202)

Short description of purpose.

#### ⚙️ Specs

- **OS:** Ubuntu 24.04.2 LTS
- **Type:** VM
- **Cores:** 4  
- **RAM:** 8 GB  
- **Storage:** 64 GB  
- **IP:** Static via DHCP Reservation
