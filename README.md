# DockWatch

## 🚀 Overview
**DockWatch** is a lightweight dashboard for monitoring Docker containers across multiple hosts.  
It uses only free and open source components and lets you build your own container image to your liking.  

DockWatch runs in an Alpine Linux container, executes a Bash script that collects container info from your Docker hosts via SSH, and displays the results in a clean HTML table.  
You can host this inside Docker itself and access the simple web interface to view all your containers.

---

## 🏗️ Architecture
- **Alpine Linux base** → small and fast
- **Bash script** → scrapes container data across hosts
- **SSH keys** → used to connect securely to remote Docker hosts
- **Nginx** → serves the dashboard HTML
- **Cron** → schedules data refresh at your chosen interval

---

## 🛠️ Getting Started
1. Make sure you have an **SSH keypair** created and access to your Docker hosts.  
2. Clone this repository and add your SSH key (`id_rsa`).  
3. Build the Docker image:

   ```bash
   docker build -t dockwatch .


docker run -d -p 8080:80 \
  -e CRON_SCHEDULE="*/5 * * * *" \
  -e TZ="America/New_York" \
  -e DOCKER_HOSTS="root@dockhost1,root@dockhost2,root@dockhost3" \
  --name dockwatch \
  dockwatch
