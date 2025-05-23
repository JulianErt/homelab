# 🏡 Ubuntu LXC `DOMUS 201`

This repository documents the setup and configuration of my homelab environment based on Proxmox VE. It serves as a platform for learning, self-hosting, testing new tools, and managing infrastructure in a reproducible way.

## ⚙️ Overview

- **Hypervisor:** [Proxmox VE](https://www.proxmox.com/en/proxmox-ve)
- **Container Type:** LXC (Lightweight Ubuntu)
- **Hostname:** `domus`
- **Purpose:** General services, sandbox testing, self-hosted apps
- **Design Goals:** Modular, secure, minimal


## 🛠️ Setup Instructions

```
# Create LXC container on Proxmox
pct create 201 local:vztmpl/ubuntu-22.04-standard_*.tar.gz \
  --hostname domus \
  --cores 2 \
  --memory 2048 \
  --net0 name=eth0,bridge=vmbr0,ip=dhcp \
  --rootfs local-lvm:10 \
  --unprivileged 1 \
  --features nesting=1

# Start the container
pct start 201

# Run initial setup (optional)
pct exec 201 -- bash -c "curl -s https://raw.githubusercontent.com/<your-username>/homelab/main/config/domus-init.sh | bash"
```
```markdown
## 🧩 Planned Services on `domus`

- [ ] Docker + Portainer
- [ ] Pi-hole (DNS-level ad blocking)
- [ ] Uptime Kuma (Status monitoring)
- [ ] NGINX or Caddy (reverse proxy)
- [ ] Syncthing (file sync)

## 🛠️ Tools in Use

| Tool         | Purpose                  |
|--------------|--------------------------|
| Proxmox VE   | Virtualization platform  |
| LXC          | Container virtualization |
| Docker       | Application management   |
| GitHub       | Version control          |