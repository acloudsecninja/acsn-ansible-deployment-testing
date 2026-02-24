# acsn-ansible-deployment-testing
# Ubuntu Docker Container Deployment with Ansible

This Ansible playbook automates the deployment of an Ubuntu Docker container on target hosts.

## Files Created

- `playbooks/deploy-ubuntu-docker.yml` - Main playbook for deploying Ubuntu Docker container
- `inventory/hosts.ini` - Inventory file for target hosts
- `requirements.yml` - Ansible collections requirements
- `ansible.cfg` - Ansible configuration file

## Prerequisites

- Ansible installed on control node
- SSH access to target hosts with sudo privileges
- Target hosts running Ubuntu/Debian

## Installing Ansible on Windows

### Option 1: Using Windows Subsystem for Linux (WSL2) - Recommended

 **Install WSL2:**
   ```powershell
   wsl --install
   ```
   This installs Ubuntu by default.

## Usage

1. Install required collections:
   ```bash
   ansible-galaxy install -r requirements.yml
   ```

2. Update the inventory file with your target hosts:
   ```ini
   [docker_hosts]
   server1 ansible_host=192.168.1.100 ansible_user=ubuntu
   ```

3. Run the playbook:
   ```bash
   ansible-playbook playbooks/deploy-ubuntu-docker.yml
   ```

## What the Playbook Does

1. Updates apt package cache
2. Installs required packages for Docker
3. Adds Docker GPG key and repository
4. Installs Docker CE and related packages
5. Starts and enables Docker service
6. Pulls Ubuntu Docker image
7. Creates and runs Ubuntu container with:
   - Name: ubuntu-container
   - Image: ubuntu:latest
   - Port mapping: 8080:80
   - Volume mount: /tmp:/host_tmp
   - Restart policy: unless-stopped

## Customization

You can modify the following variables in the playbook:
- `container_name`: Name of the Docker container (default: ubuntu-container)
- `image_name`: Docker image to use (default: ubuntu:latest)
- `container_state`: Container state (default: started)
