To set up n8n—a powerful open-source workflow automation tool—on your Proxmox server, you can choose between using an LXC container or a virtual machine (VM). Here's a step-by-step guide for both methods:([kings-guard.com](https://kings-guard.com/how-to-update-n8n-proxmox/?utm_source=chatgpt.com "How to Update n8n ProxMox: A Step-by-Step Guide for Users"))

---

## 🧰 Option 1: Install n8n in a Proxmox LXC Container (Lightweight & Efficient)

### 1. Create the LXC Container

- In the Proxmox web interface, click **Create CT**.
    
- Use an Ubuntu template (e.g., `ubuntu-22.04`).
    
- Allocate at least **2 CPUs**, **2GB RAM**, and **10GB storage**.
    
- Enable a network bridge (e.g., `vmbr0`) with DHCP or a static IP.([tecmint.com](https://www.tecmint.com/proxmox-create-container/?utm_source=chatgpt.com "How to Create a LXC Container in Proxmox - Tecmint"), [kings-guard.com](https://kings-guard.com/how-to-update-n8n-proxmox/?utm_source=chatgpt.com "How to Update n8n ProxMox: A Step-by-Step Guide for Users"))
    

![[proxmox n8n.png]]

```
  
()

[

](https://192.168.2.222:8006/#)

[

](https://192.168.2.222:8006/#)

[

](https://192.168.2.222:8006/#)

[

](https://192.168.2.222:8006/#)

[

](https://192.168.2.222:8006/#)

[

](https://192.168.2.222:8006/#)

[

](https://192.168.2.222:8006/#)

Task viewer: CT 106 - Create

OutputStatus

Stop

Download

WARNING: You have not turned on protection against thin pools running out of space.  
WARNING: Set activation/thin_pool_autoextend_threshold below 100 to trigger automatic extension of thin pools before they get full.  
Logical volume "vm-106-disk-0" created.  
WARNING: Sum of all thin volume sizes (<556.01 GiB) exceeds the size of thin pool pve/data and the size of whole volume group (<446.63 GiB).  
Creating filesystem with 4194304 4k blocks and 1048576 inodes  
Filesystem UUID: 749dc722-24c3-457c-bb89-a369949c096f  
Superblock backups stored on blocks:  
32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,  
extracting archive '/var/lib/vz/template/cache/ubuntu-22.04-standard_22.04-1_amd64.tar.zst'  
Total bytes read: 508579840 (486MiB, 267MiB/s)  
Detected container architecture: amd64  
Creating SSH host key 'ssh_host_ed25519_key' - this may take some time ...  
done: SHA256:3wsKrwuHniGIyQF+mESQnuSlogQBUVw87UlylxvVsl8 root@n8n  
Creating SSH host key 'ssh_host_ecdsa_key' - this may take some time ...  
done: SHA256:mFgjdG0sKX1BA5sACJE31s4iWFOJAKLrKwnbbXBV7Ik root@n8n  
Creating SSH host key 'ssh_host_dsa_key' - this may take some time ...  
done: SHA256:HzEhWiezK0zw2aUHYEzDnJv8Ho+t8b1iMXbTrqpak1k root@n8n  
Creating SSH host key 'ssh_host_rsa_key' - this may take some time ...  
done: SHA256:d5L80fsUhHhyFAEVmfRQDuJ5kO3oYh5LC15nUy/OGcY root@n8n  
TASK OK
```
### 2. Access the Container

- Start the container and open the **Console** tab or connect via SSH.([tecmint.com](https://www.tecmint.com/proxmox-create-container/?utm_source=chatgpt.com "How to Create a LXC Container in Proxmox - Tecmint"))
    
![[proxmox n8n-1.png]]
### 3. Install Dependencies and n8n

Run the following commands inside the container:

```bash
apt update && apt upgrade -y
apt install -y curl gnupg2 ca-certificates lsb-release
curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
apt install -y nodejs
npm install -g n8n pm2
```

[[linux nameserver fix ]]

### 4. Start n8n

```bash
pm2 start n8n
pm2 startup
pm2 save
```

This setup ensures n8n starts automatically on container boot.([community.n8n.io](https://community.n8n.io/t/setting-up-n8n-on-proxmox-vm-issues/60499?utm_source=chatgpt.com "Setting Up n8n on ProxMox VM Issues - Questions"))

```
https://192.168.2.222:8006/?console=lxc&xtermjs=1&vmid=106&vmname=n8n&node=workstation&cmd=
```


[[access to pod n8n]]
## 🖥️ Option 2: Install n8n in a Proxmox VM (For Full Isolation)

### 1. Create a VM

- Use an Ubuntu ISO (e.g., `ubuntu-22.04-server.iso`).
    
- Allocate at least **2 CPUs**, **2GB RAM**, and **10GB storage**.([kings-guard.com](https://kings-guard.com/how-to-update-n8n-proxmox/?utm_source=chatgpt.com "How to Update n8n ProxMox: A Step-by-Step Guide for Users"))
    

### 2. Install Ubuntu

- Boot the VM from the ISO and follow the installation prompts.
    

### 3. Install Docker and Docker Compose

Inside the VM:

```bash
apt update && apt upgrade -y
apt install -y docker.io docker-compose
```

### 4. Set Up n8n with Docker Compose

Create a `docker-compose.yml` file:

```yaml
version: "3.7"
services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=securepassword
    volumes:
      - ~/.n8n:/home/node/.n8n
    restart: always
```

Start the service:

```bash
docker-compose up -d
```

Access n8n at `http://<VM_IP>:5678`.([community.n8n.io](https://community.n8n.io/t/n8n-install-on-proxmox-vm-with-ngrok-and-trying-to-use-telegram-webhook/79986?utm_source=chatgpt.com "N8N install on Proxmox VM with ngrok and trying to use telegram ..."))

---

## 🔄 Updating n8n

- **For LXC (npm installation):**
    
    ```bash
    pm2 stop n8n
    npm update -g n8n
    pm2 start n8n
    ```
    

- **For Docker (VM installation):**
    
    ```bash
    docker pull n8nio/n8n:latest
    docker-compose down
    docker-compose up -d
    ```
    

---

## 🔐 Securing n8n

- **HTTPS:** Use a reverse proxy like Nginx or Traefik with Let's Encrypt for SSL certificates.
    
- **Authentication:** Enable basic authentication by setting `N8N_BASIC_AUTH_ACTIVE=true` and providing a username and password.
    
- **Public Access:** If exposing n8n to the internet, ensure proper firewall rules and consider using tools like ngrok for secure tunnels.([community.n8n.io](https://community.n8n.io/t/n8n-install-on-proxmox-vm-with-ngrok-and-trying-to-use-telegram-webhook/79986?utm_source=chatgpt.com "N8N install on Proxmox VM with ngrok and trying to use telegram ..."))
    

---

## 📺 Video Tutorial

For a visual walkthrough, you might find this video helpful:

[How to Install n8n on Proxmox](https://www.youtube.com/watch?v=J1cpJRuTHwE&utm_source=chatgpt.com)

---

Feel free to ask if you need further assistance or have specific requirements for your n8n setup!