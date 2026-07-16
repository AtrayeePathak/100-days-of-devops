# Day 11 — Azure Resource Manager Templates in 60 Minutes

**Date:** 2026-07-16

## What I set out to learn

Understand Azure Resource Manager (ARM) templates, how they work, and how they differ from Bicep and Terraform.

## What I did

- Watched the video on ARM templates and focused on how Azure deployments can be defined as code
- Learned that ARM templates are JSON-based definitions used by Azure Resource Manager to create and manage resources
- Compared ARM templates with Bicep, which provides a cleaner and simpler syntax
- Compared ARM and Bicep with Terraform, especially in terms of declarative infrastructure management and portability
- Revisited the idea that infrastructure should be created through templates instead of manual clicks in the Azure portal

## What I learned / key takeaways

- ARM templates are the native Azure way to define infrastructure as code
- Bicep is a more human-friendly language that compiles to ARM templates
- Terraform is also powerful, but it is more cloud-agnostic and works across multiple providers
- Using templates makes deployments repeatable, easier to version control, and less error-prone
- For Azure-first work, Bicep is often a cleaner choice than writing raw ARM JSON

## Resources

- Azure Resource Manager documentation
- Bicep documentation
- Azure zero-to-hero repo Day 11 notes
- YouTube video: Azure Resource Manager Templates in 60 Minutes

## Next steps

Practice writing a small Bicep or ARM template to deploy a resource group, storage account, or virtual machine.
