# Ansible Playbook for Kubernetes Cluster Setup

This repository contains Ansible playbooks to automate the setup of various components required for a Kubernetes cluster. The playbooks include tasks for setting up Flux, Helm, a load balancer, SOPS (Secrets OPerationS), and a container registry.

## Playbooks Overview

### 1. `Flux Setup`
- **Description:** Sets up Flux, a GitOps tool for managing and deploying Kubernetes configurations from a Git repository.
- **Hosts:** `control-planes`
- **Included Tasks:** `flux/setup.yaml`

### 2. `Helm Setup`
- **Description:** Configures Helm, a package manager for Kubernetes, enabling easy deployment of applications and services.
- **Hosts:** `control-planes`
- **Included Tasks:** `helm/setup.yaml`

### 3. `Load Balancer Setup`
- **Description:** Sets up a load balancer to distribute traffic across your Kubernetes cluster nodes.
- **Hosts:** `control-planes`
- **Included Tasks:** `load_balancer/setup.yaml`

### 4. `SOPS Setup`
- **Description:** Configures SOPS, a tool for managing secrets and encrypting/decrypting files securely in your Kubernetes environment.
- **Hosts:** `control-planes`
- **Included Tasks:** `sops/setup.yaml`

### 5. `Registry Setup`
- **Description:** Sets up a container registry on all nodes, allowing for the storage and management of container images.
- **Hosts:** `all`
- **Included Tasks:** `registry/setup.yaml`

## Usage

1. **Clone the repository:**

   ```bash
   git clone https://github.com/dave-andrew/k8s-starter-config.git
   cd k8s-starter-config

2. **Create Ansible Configuration:**
   ```bash
   vi /etc/ansible/ansible.cfg
   
   [defaults]
   inventory=/etc/ansible/hosts
   cache=None
   host_key_checking = False
   remote_user = root

3. **Create Default Ansible Inventory:**
   ```bash
   vi /etc/ansible/hosts

   [control-planes]
   10.22.77.81
   10.22.77.82
   10.22.77.83

   [workers]
   10.22.77.90
   10.22.77.91
   10.22.77.92

   [all:vars]
   registry_url="registry-url.net"
   registry_port="5000"
   virtual_ip="10.22.77.89"

2. **Execute the playbook command:**
   ```bash
   ansible-playbook playbook.yaml