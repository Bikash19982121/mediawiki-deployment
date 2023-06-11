# Deploying Mediawiki app into kubernetes cluster using helm chart

 This Helm chart deploys a Wikimedia application along with a MySQL database in a Kubernetes cluster.

## Prerequisites
- Kubernetes cluster
- Helm 3.x
## Installation
1. Clone the repository:
 ```bash
git clone https://github.com/Bikash19982121/mediawiki-deployment.git

```
2. Go inside Ansible-k8s-setup directory and Modify the inventory file dev_host.ini to specify the target host or group of hosts to install and configure kubernetes cluster.


3. Run the playbook to install Nginx, kubernetes and mysql:

```bash
ansible-playbook kubernetes

```
4. Change directory to the chart:
 ```bash
cd helm-chart
```
3. Modify the values.yaml file to configure the chart according to your requirements. Update the MySQL database credentials, storage settings, and any other necessary parameters.
4. Install the chart using Helm:
```bash
helm install wikichart .
```
This will deploy the Wikimedia application and MySQL database in your Kubernetes cluster.
5. Verify the deployment:
```bash
kubectl get pods
kubectl get services
```
Ensure that the pods and services are created and running successfully.

You can access the application http://<server-ip>:30080/mediawiki
  
6. Copy the Downloaded LocalSettings.php file into the  application container using the following command:
  ```bash
kubectl cp ./LocalSettings.php <pod-name>:/var/www/html/mediawiki/LocalSettings.php
```
  
