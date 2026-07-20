# Day 12 — Azure IAM Basics and Managed Identities Demo

**Date:** 2026-07-20

## What I set out to learn

Understand the basics of Azure Identity and Access Management (IAM), including roles, permissions, and managed identities in Microsoft Entra ID.

## What I did

- Learned about Azure IAM and why it is important for access control in cloud environments
- Reviewed the difference between authentication and authorization in Azure
- Looked at Role-Based Access Control (RBAC) and how roles are assigned to users, groups, and services
- Studied managed identities and why they are useful for allowing Azure services to access other Azure resources securely
- Revisited the idea that secrets do not need to be embedded in applications when managed identities are available

## What I learned / key takeaways

- Azure IAM controls who can do what on Azure resources
- RBAC is the main model used to assign permissions in a least-privilege way
- Managed identities allow Azure services to authenticate to other Azure services without storing credentials manually
- Microsoft Entra ID is the identity platform behind modern Azure access control
- A strong IAM setup is essential for security, governance, and operational safety

## Resources

- Azure IAM documentation
- Azure RBAC documentation
- Managed identities for Azure resources documentation
- Microsoft Entra ID documentation
- YouTube video: Azure IAM from Basics | Azure Managed Identities Demo with Microsoft Entra

## Next steps

Practice assigning RBAC roles to a resource and explore how a managed identity can access a storage account or Key Vault securely.
