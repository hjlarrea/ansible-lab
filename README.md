# 🛠️ Ansible Lab with Docker Compose

## ⚡ Quick Start

```bash
# 0. Requirements
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/index.html) (`brew install ansible` or `pipx install ansible`)

# 1. Clone the repo and enter it
git clone https://github.com/<your-username>/ansible-lab.git
cd ansible-lab

# 2. Generate SSH keys for the lab
mkdir -p keys && ssh-keygen -t ed25519 -f keys/id_ed25519 -N ""

# 3. Build and start the lab environment
export PUBKEY="$(cat keys/id_ed25519.pub)"
docker compose up -d --build

# 4. Run Ansible playbooks (from the ansible folder)
cd ansible
ansible all -m ping
ansible-playbook playbooks/web.yml
```

## Introduction

This repository contains a simple laboratory to practice [Ansible](https://docs.ansible.com/) without needing real servers.  
It provides a lightweight environment with:

It provides a lightweight environment with:
	•	1 Ansible control node (your own machine, where you run ansible)
	•	2 managed nodes (Docker containers reachable via SSH)
	•	Iniitial playbooks to test connectivity and install a basic service (Nginx). You can build beyond these to practice.

## 📂 Repository Structure

```
ansible-lab/
├─ ansible/ # Ansible configuration, inventory, playbooks
│  ├─ ansible.cfg
│  ├─ inventory.ini
│  └─ playbooks/
│     ├─ ping.yml
│     └─ web.yml
├─ docker/ # Docker build context for managed nodes
│  └─ Dockerfile
├─ docker-compose.yml # Orchestrates lab nodes
├─ keys/ # SSH keypair for lab access
└─ README.md
```

## 🧪 Included Playbooks
	•	ping.yml → Checks basic Ansible connectivity.
	•	web.yml → Installs Nginx and ensures it’s running.