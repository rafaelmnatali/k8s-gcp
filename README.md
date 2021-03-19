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
    # use this section to enter GCP related information
    zone: europe-west2-c
    region: europe-west2
    project_id: <gcp-project-id>
    gcloud_sa_path: "~/gcp-credentials/service-account.json"
    credentials_file: "{{ lookup('env','HOME') }}/{{ gcloud_sa_path }}"
    gcloud_service_account: service-account@project-id.iam.gserviceaccount.com

    # use the section below to enter k8s cluster related information
    cluster_name: <name for your k8s cluster>
    initial_node_count: 1
    disk_size_gb: 100
    disk_type: pd-ssd
    machine_type: n1-standard-2
```

Refer to Ansible documentation on [How to build your inventory](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html) for more information.

## How to use this repository

### Provision Kubernetes

Execute the following command to provision the `Kubernetes` cluster:

`ansible-playbook ansible/create-gke.yml -i ansible/inventory/<your-inventory-filename>`

**Output:**

```text
PLAY [create infra] ****************************************************************

TASK [network : create GCP network] ************************************************
changed: [localhost]

TASK [k8s : create k8s cluster] ****************************************************
changed: [localhost]

TASK [k8s : create k8s node pool] **************************************************
changed: [localhost]

PLAY RECAP *************************************************************************
localhost: ok=3  changed=3  unreachable=0  failed=0  skipped=0  rescued=0  ignored=0 
```

### Connecting to the Kubernetes cluster

Use the [gcloud](https://cloud.google.com/sdk/gcloud) command-line tool to connect to the Kubernetes cluster:

`gcloud container clusters get-credentials <cluster_name> --zone <zone> --project <project_id>`

_Note:_ replace the variables with the values used in the inventory file. Also, It's possible to retrieve this command from the `GCP` console.

**Output:**

```text
Fetching cluster endpoint and auth data.
kubeconfig entry generated for devops-platform.
```

### Using the Kubernetes cluster

After connecting to the cluster use the [kubectl](https://kubernetes.io/docs/reference/kubectl/overview/) command-line tool to control the cluster.

```text
kubectl get nodes
NAME                                                STATUS   ROLES    AGE   VERSION
gke-<cluster_name>-node-pool-e058a106-zn2b          Ready    <none>   10m   v1.18.12-gke.1210
```

### Cleaning up

Execute the following command to destroy the `Kubernetes` cluster:

`ansible-playbook ansible/destroy-gke.yml -i ansible/inventory/<your-inventory-filename>`

**Output:**

```text
PLAY [destroy infra] *********************************************************************

TASK [destroy_k8s : destroy k8s cluster] *************************************************
changed: [localhost]

TASK [destroy_network : destroy GCP network] *********************************************
changed: [localhost]

PLAY RECAP *******************************************************************************
localhost: ok=2   changed=2   unreachable=0   failed=0   skipped=0   rescued=0   ignored=0 
```

## References

- [Ansible Google Cloud Modules](https://docs.ansible.com/ansible/latest/collections/google/cloud/index.html)

## Next Steps
