# tech-challenge-maximilian

This repository contains Ansible playbooks to install and configure all services required to deploy two simple web servers to local minikube clusters and monitor them with kuma uptime.

## Prerequisites

The playbooks will install the required software on your system. Installation is only tested on Linux Ubuntu. You can install the required software manually and run the playbooks with `--tags noinstall`, e.g. `ansible-playbook -i inventories/main.yaml playbooks/docker/docker.yaml --tags noinstall`.

If you opt for manual installation please ensure that:

- Docker is [installed](https://docs.docker.com/engine/install/). Also make sure your current user can [manage docker without sudo](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user).
- Minikube is [installed](https://minikube.sigs.k8s.io/docs/start/)
- Act is [installed](https://nektosact.com/installation/index.html)

## Dependencies

### ansible-uptime-kuma

Please follow the [installation instructions](https://github.com/lucasheld/ansible-uptime-kuma?tab=readme-ov-file#installation) provided by the repo.

### Note:

Add the python path of your virtual environment to the inventory file located at `inventories/main.yaml` under `all.hosts.localhost.ansible_python_interpreter` in order for the plays to have access to installed dependencies.

## Playbooks

### Docker

The docker playbook located at `playbooks/docker/docker.yaml` installs docker and configures a local image registry.

Run with: `ansible-playbook -i inventories/main.yaml playbooks/docker/docker.yaml`

### Minikube

The minikube playbook located at `playbooks/minikube/minikube.yaml` installs minikube. Then it starts and configures three minikube clusters one for each environment.

Run with: `ansible-playbook -i inventories/main.yaml playbooks/minikube/minikube.yaml`

### Act

The act playbook located at `playbooks/act/act.yaml` installs act and prepares the runner image in order to run GitHub Actions locally.

Run with: `ansible-playbook -i inventories/main.yaml playbooks/act/act.yaml`

### Kuma Uptime

The kuma playbook located at `playbooks/kuma/kuma.yaml` installs and configures Kuma Uptime to monitor the services deployed to the different environments.

Run with: `ansible-playbook -i inventories/main.yaml playbooks/kuma/kuma.yaml`

## Run

### 1. Deployment environment:

Run the **Docker**, **Minikube** and **Act** playbooks.

### 2. Apps

Clone the repositories of two test apps [hello](https://github.com/Maxi-Teme/tech-challenge-hello) and [bye](https://github.com/Maxi-Teme/tech-challenge-bye) from GitHub

```sh
git clone https://github.com/Maxi-Teme/tech-challenge-hello.git
git clone https://github.com/Maxi-Teme/tech-challenge-bye.git
```

and follow the instructions of their READMEs under the section **deploy locally**.

### 3. Monitoring

After the apps are deployed successfully on minikube, run the **Kuma Uptime** playbook.
