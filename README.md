# Secure Nginx Web Server Deployment on Azure Linux VM

## Project Purpose
The goal of this project is to deploy, configure, and secure a public-facing Nginx web server inside a simulated enterprise cloud environment using Microsoft Azure and Ubuntu Linux. It demonstrates hands-on experience with cloud networking, remote secure administration, and live infrastructure troubleshooting.

### Project Highlights
* **Cloud Infrastructure Provisioning:** Successfully deployed an Ubuntu Linux Virtual Machine (`vm-web-01`) within the Microsoft Azure environment.
* **Web Server Administration:** Installed, configured, and verified an active Nginx web server to handle external web requests.
* **Network Security & Firewalls:** Configured Network Security Groups (NSGs) to tightly manage inbound traffic channels—authorizing Port 22 for secure backend administration (SSH) and Port 80 for public-facing web traffic (HTTP).
* **Infrastructure Troubleshooting:** Diagnosed and resolved real-world connection barriers, including isolating local desktop application firewalls (VPN kill-switches) and dynamically modifying Azure NSG inbound rules to align with network handoffs.

---

## Relevant Tools & Technologies
* **Cloud Platform:** Microsoft Azure (Virtual Machines, Network Security Groups, Virtual Networks)
* **Operating System:** Linux (Ubuntu 24.04 LTS)
* **Web Server Software:** Nginx
* **Administration Protocols:** SSH (Secure Shell), Command Prompt/Terminal, Nano Editor

---

## Step-by-Step Implementation

### Phase 1: Virtual Machine Provisioning
1. Created an Ubuntu 24.04 LTS Virtual Machine in the Azure Portal named `vm-web-01`.
2. Generated a secure SSH key pair (`vm-web-0_key.pem`) for administrative login.
3. Assigned a static/public IP address (`20.49.2.244`) to the cloud network interface.

### Phase 2: Server Configuration & Nginx Deployment
1. Established a secure remote connection to the cloud instance using SSH via the local terminal.
2. Updated the Linux package management system and deployed the Nginx server package.
3. Configured and validated the core `default` site block parameters using the Nano editor:
   ```nginx
   server {
       listen 80 default_server;
       listen [::]:80 default_server;
       root /var/www/html;
       index index.html;
       server_name _;
       location / {
           try_files $uri $uri/ =404;
       }
   }
