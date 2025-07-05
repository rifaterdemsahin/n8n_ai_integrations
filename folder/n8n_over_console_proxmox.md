Here’s an improved and reliable script for installing **n8n** in an LXC on Proxmox, fully supported on Proxmox VE 8.4+:

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/ct/n8n.sh)"
```

---

### ✅ Why this script rocks

* **Updated for Proxmox 8.x** — it won’t stumble over missing templates or version checks.
* **Full LXC setup** — creates an unprivileged Debian 12 container, installs Node.js, npm, and n8n, configures a systemd service, then outputs your access URL.
* **Actively maintained** — part of the community-driven Proxmox VE Helper‑Scripts, a live and growing repository ([github.com][1], [i12bretro.wordpress.com][2]).

---

### 🎥 Want a step-by-step walkthrough?

Here’s a helpful video guide to installing n8n on Proxmox:

[Installing n8n on Proxmox with Community Script](https://www.youtube.com/watch?v=L5ZaVQBxRPA&utm_source=chatgpt.com)

---

### 🔧 Dealing with download/template issues

If the template download fails:

1. Double-check your network and storage settings in Proxmox.
2. Manually download the Debian 12 template via CLI:

   ```bash
   pveam update
   pveam download local debian-12-standard_12.7-1_amd64.tar.zst
   ```
3. Run the install script again.

The updated script ensures templates are obtained cleanly — no half-failed downloads.

---

### 🔄 Next steps post-install

* **Enable HTTPS**: Set up a reverse proxy (e.g., Nginx, Traefik, or Nginx Proxy Manager) and configure `N8N_HOST`, `N8N_PROTOCOL`, and `WEBHOOK_URL` as env vars. For guidance see n8n forum tips ([github.com][3]).
* **Secure access**: Add basic auth or OAuth via `N8N_BASIC_AUTH_*` env vars before first launch.
* **Install community packages (like MCP or Puppeteer)**: Enter the container’s shell and `npm install -g <package>`, then restart the n8n service.

---

### ✅ TL;DR

Use the community script command above for a seamless install. If you hit template download issues, fetch the Debian 12 image manually using `pveam`. Once the container is up, configure HTTPS, add required plugins, and enjoy your powerful self-hosted automation! 🚀

Let me know if you want help with reverse proxy setup, HTTPS, or adding plugins inside the container.

[1]: https://github.com/community-scripts/ProxmoxVE?utm_source=chatgpt.com "Proxmox VE Helper-Scripts (Community Edition) - GitHub"
[2]: https://i12bretro.wordpress.com/2023/07/31/running-a-debian-12-bookworm-vm-in-proxmox-ve/?utm_source=chatgpt.com "Running a Debian 12 Bookworm VM in Proxmox VE"
[3]: https://github.com/community-scripts/ProxmoxVE/issues/2034?utm_source=chatgpt.com "n8n LXC installation fail · Issue #2034 · community-scripts/ProxmoxVE"
