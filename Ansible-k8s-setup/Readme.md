# Ansible Kubernetes Installation Playbook
This Ansible playbook is designed to automate the installation of Kubernetes on Ubuntu.

## Prerequisites

- A compatible Linux hosts:  2 GB or more of RAM per machine and 2 CPUs or more 
- 3 - Ubuntu 20.04 LTS Serves:  1x Manager (4GB RAM, 2 vCPU)t2.medium type, 2x Workers (1 GB, 1 Core) t2.micro type 
- Full network connectivity between all machines in the cluster 
- Unique hostname for each host. Change hostname of the machines using hostnamectl. For master nodes, run`hostnamectl set-hostname master`. For slaves, run `hostnamectl set-hostname slave-01`  `hostnamectl set-hostname slave-02` 
- Certain ports are open on your machines(https://kubernetes.io/docs/reference/ports-and-protocols/)
  - On Master Node
	```
	6443/tcp for Kubernetes API Server
	2379-2380 for etcd server client API
	6783/tcp,6784/udp for Weavenet CNI
	10248-10260 for Kubelet API, Kube-scheduler, Kube-controller-manager, Read-Only Kubelet API, Kubelet health
	80,8080,443 Generic Ports
	30000-32767 for NodePort Services
	```
  - On Slave Nodes
	```
	6783/tcp,6784/udp for Weavenet CNI
	10248-10260 for Kubelet API etc
	30000-32767 for NodePort Services
	```

# Project Structure

1. `ansible.cfg` is the configuration file for Ansible. It contains settings such as the location of the inventory file,private key,role path, extra variable etc.
2. `inventory/host.ini` is the inventory file that defines the hosts that Ansible will manage. It lists the IP addresses or domain names of the hosts and groups them into categories.
3. `roles/` is a directory that contains all the roles for the Ansible project. In this project, there's only multiple role named nginx,kubernetes,mysql
5. `kubernetes` is the main playbook that will be execute the kubernetes and k8s_upgrade role.
5. `group_vars` directory to store environment-specific variable values for your inventory groups. This can be useful for defining variables that are specific to certain environments, such as development, staging, and production.

# Ansible Configuration File


# Requirements
1. Ansible 2.10 or later
2. Ubuntu operating system (tested on Ubuntu 20.04)
3. Role Variables- You can modify these Role variables in the vars/main.yml file to customize the Software installation.

# Dependencies
NA

# Usage

1. Clone the repository to your local machine:

```bash
git clone https://github.com/bikashamdocs/ansible-setup.git
```

2. Modify the inventory file prod_host.ini or dev_host.ini to specify the target host or group of hosts to install required software.


3. Run the playbook to install Nginx, kubernetes and mysql:

```bash
ansible-playbook kubernetes

```


# Using Key-Based Authentication with Ansible:

Prerequisites:
 1. A remote server that you want to manage with Ansible
 2. A user account on the remote server with sudo privileges

Step 1: Generate an SSH key pair

```bash
ssh-keygen
```
By default, this will create a 2048-bit RSA key pair in the ~/.ssh directory.

Step 2: Copy the public key to the remote server using the ssh-copy-id command:

```bash
ssh-copy-id remote_user_name@remote_server_ip_address
```
Step 3: Modify your Ansible inventory file
In your Ansible inventory file, modify the entry for the remote server to use the SSH key. Replace remote_user_name with the username of the remote user, and /path/to/private/key with the path to the private key file on your Ansible control node.


# Testing
1. This role includes a tests directory with a sample inventory and test playbook. You can run the tests using the following command:

```bash
ansible-playbook tests/test.yml -i tests/inventory
```

# License

NA


# Author Information
This role was created by Bikash.
