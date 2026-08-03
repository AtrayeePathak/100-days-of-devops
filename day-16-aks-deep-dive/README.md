# Day 16 — Azure Kubernetes Services (AKS Deep Dive)

**Date:** 2026-08-03

## What I set out to learn

Understand Azure Kubernetes Service (AKS) architecture and compare managed AKS against self-managed Kubernetes clusters.

## What I did

- Explored the AKS shared responsibility model (managed control plane vs worker node pools)
- Studied core AKS features (Azure CNI, Entra ID RBAC, autoscaling, CSI storage)
- Compared AKS vs self-managed Kubernetes across maintenance, cost, and scaling

## AKS Deep Dive

- **Managed Control Plane:** Azure handles the API Server, `etcd`, scheduler, and controller manager automatically (zero control plane management fee for standard clusters).
- **Worker Node Pools:** Customer manages application node pools (VM Scale Sets), Kubelet, container runtime (`containerd`), and Kube-proxy.
- **Key Features:** Azure CNI networking, Microsoft Entra ID RBAC, Cluster Autoscaler & HPA, Azure Key Vault secrets integration, and seamless ACR integration.

## AKS vs Self-Managed Kubernetes

| Feature | Azure Kubernetes Service (AKS) | Self-Managed Kubernetes |
| :--- | :--- | :--- |
| **Control Plane** | Managed & backed up by Azure | Manually built & managed (`kubeadm`/`kops`) |
| **Ops Overhead** | Low (Azure handles control plane HA/patches) | High (Manual master node maintenance & etcd backups) |
| **Cost** | Pay only for worker node VMs | Pay for master nodes + worker nodes + maintenance labor |
| **Upgrades** | 1-click / automated rolling upgrades | Manual step-by-step master node drain & upgrade |
| **Integrations** | Native (ACR, Key Vault, Entra ID, Azure VNet) | Custom cloud driver setup required |

## Key Takeaways

- Managed AKS offloads heavy control plane maintenance, allowing teams to focus on application deployment.
- Self-managed Kubernetes is best suited for strict air-gapped environments or where complete control over API server internals is mandatory.

## Resources

- [Official Azure Kubernetes Service (AKS) Documentation](https://learn.microsoft.com/en-us/azure/aks/)
- [Kubernetes Official Documentation](https://kubernetes.io/docs/)
