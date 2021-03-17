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

## Ansible Inventory

Create a `yaml` file in the `inventory` folder to allow Ansible to interact with your `GCP` environment.

Here is a sample file:

```yaml
all:
  vars:
    zone: europe-west2-c
    region: europe-west2
    project_id: <gcp-project-id>
    gcloud_sa_path: "~/gcp-credentials/service-account.json"
    credentials_file: "{{ lookup('env','HOME') }}/{{ gcloud_sa_path }}"
    gcloud_service_account: service-account@project-id.iam.gserviceaccount.com
    cluster_name: <name for your k8s cluster>
```

Refer to Ansible documentation on [How to build your inventory](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html) for more information.

## References

- [Ansible Google Cloud Modules](https://docs.ansible.com/ansible/latest/collections/google/cloud/index.html)

## Next Steps
