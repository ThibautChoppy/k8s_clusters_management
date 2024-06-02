# k8s_clusters_management `[v0.1 - Unstable]`

This fluxcd repository manage a kubernetes cluster

## Prerequisites

To run this project, you need a running kubernetes cluster and an smb or nfs server.

Home Lab :
```
- Proxmox Server (64 Core - 128 Gb RAM)
    - OpenMediaVault NFS server
    - Kubernetes Cluster
        - Master
            - Node_1
            - Node_2
```

## Get Started

### Dependencies

- NFS server for cluster storage management - *Automatic NFS server configuration to come*
- Running Kubernetes cluster - *[k8s_baremetal_ansible](https://github.com/ThibautChoppy/k8s_baremetal_ansible/tree/main) for automatic configuration*
- Github Personnal Access Token - *with read/write repository permission*
- Admin kubeconfig file in `~/.kube/config`

### Configuration update

Once the environment has been set up, update the manifests in this repository with the configuration of your cluster.
> `grep -r "FIXME"` to see the needed changes

### FluxCD Bootstrap

Run this command to synchronize FluxCD with your repository
> Don't forget to update command informations
```
flux bootstrap github --token-auth --owner=Your-Organisation --repository=k8s_clusters_management --branch=main --path=clusters/cluster-0 --personal --components-extra=image-reflector-controller,image-automation-controller
```
When initializing the cluster, you will need to initialize the Hashicorp Vault to continue synchronization.

>[k8s_cluster_bootstrap](https://github.com/ThibautChoppy/k8s_clusters_bootstrap/tree/main) for automatic Vault configuration\
*WARNING: Uncomplete & Unstable version, improvements to come*

#### Your cluster is now configured !

### Application deployment

Update the manifests in the `apps/stack` and `apps/application` for your own deployments.
Once this is done, simply uncomment the lines in `cluster/cluster-0/apps.yaml` to activate synchronization.

## Built With

| Package                                                       | Usage                                             | Version |
| :------------------------------------------------------------ | :------------------------------------------------ | :------ |
| [Proxmox](https://www.proxmox.com/en/)                        | Level 1 hypervisor                                | 8.1.10  |
| [Kubernetes](https://kubernetes.io/)                          | Docker container orchestrator                     | 1.28.6  |
| [FluxCD](https://fluxcd.io/flux/)                             | GitOps tool for IaC synchronization               | 2.3.0   |

## Authors

* **Thibaut Choppy** - *Initial work* - [Linkedin](https://www.linkedin.com/in/thibaut-choppy/)
