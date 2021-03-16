# Kubernetes on GCP

[Kubernetes](https://kubernetes.io) is a widely used system to manage containerised applications.
[GCP](https://www.cloud.google.com) is the computing services platform powered by Google.

This tutorial intends to demonstrate how one can use [Infrastructure as Code (IaC)](https://docs.microsoft.com/en-us/azure/devops/learn/what-is-infrastructure-as-code) to automate the provision of a `Kubernetes` cluster running on `GCP`.

> The designed solution is for learning purposes. Hence, don't treat as production-ready.

## Ansible

[Ansible](https://www.ansible.com) is the tool of choice to implement automation. Ansible is one of the most utilised automation tools in the market and allows the creation of the automation necessary to run the `Kubernetes cluster.

## Requisites

- [Installing Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- [Ansible Google Cloud Platform Guide](https://docs.ansible.com/ansible/latest/scenario_guides/guide_gce.html)
- [Installing Python](https://www.python.org/downloads/)

## Environment

The local environment used to test the scripts had the following software:

| Software | Version |
|--|--|
| macOS BigSur | 11.2.1 |
| Ansible | 3.1.0 |
| Python | 3.8.2 |

## Next Steps
