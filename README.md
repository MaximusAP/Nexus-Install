Nexus Repository Installation using Ansible
Project Overview

This project automates the installation and configuration of Sonatype Nexus Repository Manager on Ubuntu using Ansible.

The goal is to provide a repeatable and automated deployment process for Nexus in a Home Lab or Enterprise Environment.

Features
Automated Nexus installation
Automated Nexus service configuration
Automated Nexus startup using systemd
Idempotent Ansible playbook
Easy rebuild after VM failure
GitHub-friendly project structure
Technologies Used
Ansible
Ubuntu 24.04 LTS
Sonatype Nexus Repository Manager
VMware vSphere
Linux Systemd
Project Structure
Nexus-Install/
├── inventory.ini
├── install-nexus.yml
└── README.md
Prerequisites

Before running this project ensure:

Ubuntu VM is deployed
SSH connectivity is working
Ansible is installed
Sudo privileges are available
Internet access is available for Nexus download
Verify Connectivity
ansible -i inventory.ini nexus -m ping

Expected Result:

pong
Execute Installation
ansible-playbook -i inventory.ini install-nexus.yml

The playbook performs the following:

Installs required packages
Creates Nexus service account
Downloads Nexus Repository Manager
Extracts Nexus binaries
Creates Nexus data directories
Configures Nexus service
Starts Nexus automatically
Access Nexus

After successful deployment:

http://<NEXUS_IP>:8081
Retrieve Initial Admin Password
sudo cat /opt/sonatype-work/nexus3/admin.password

Login:

Username: admin
Password: <admin.password>
Docker Registry Configuration

Create a Docker Hosted Repository:

Settings
└── Repositories
    └── Create Repository
        └── docker(hosted)

Recommended Configuration:

Repository Name : docker-hosted
HTTP Port       : 8082
Deployment      : Allow redeploy
Docker Client Configuration

Example Docker daemon configuration:

{
  "insecure-registries": [
    "<NEXUS_IP>:8082"
  ]
}

Restart Docker:

sudo systemctl restart docker
Testing Docker Push
docker login <NEXUS_IP>:8082

docker tag nginx <NEXUS_IP>:8082/nginx:test

docker push <NEXUS_IP>:8082/nginx:test
CI/CD Integration

This Nexus deployment can be integrated with:

GitHub
Jenkins
Docker
Kubernetes
Rancher

Typical Flow:

GitHub
   ↓
Jenkins Pipeline
   ↓
Docker Build
   ↓
Nexus Repository
   ↓
Kubernetes Deployment
Benefits
Repeatable deployment
Faster recovery after VM failures
Infrastructure as Code approach
Reduced manual configuration
Enterprise-style repository management
Future Enhancements
Nexus SSL Configuration
Docker Proxy Repository
Docker Group Repository
Maven Repository
Helm Repository
Backup Automation
Monitoring Integration
Author

Maximus

Home Lab DevOps Platform

Built using Infrastructure as Code and Automation principles.
