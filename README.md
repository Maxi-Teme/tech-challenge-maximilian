# tech-challenge-maximilian

This repository contains Ansible playbooks to install and configure all services required to deploy two simple web servers to local minikube clusters and monitor them with kuma uptime.

## Config

Add the python path of your virtual environment to the inventory file located at `inventories/main.yaml` under `all.hosts.localhost.ansible_python_interpreter` in order for the plays to have access to installed dependencies.

## Dependencies

### ansible-uptime-kuma: https://github.com/lucasheld/ansible-uptime-kuma

`ansible-galaxy collection install lucasheld.uptime_kuma`

## Playbooks

### Docker

The docker playbook located at `playbooks/docker/docker.yaml` ensures that docker is installed and configures a local image registry.

### Minikube

The minikube playbook located at `playbooks/minikube/minikube.yaml` installs, starts and configures a minikube cluster in docker for the environment specified with the respective inventory.

### Act

The act playbook located at `playbooks/act/act.yaml` installs act in order to run GitHub Actions locally.

### Kuma Uptime

The kuma playbook located at `playbooks/kuma/kuma.yaml` installs kuma uptime to monitor the services deployed to the different environments.
