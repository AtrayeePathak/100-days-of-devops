# Day 02 — Azure Networking Demo

**Date:** 2026-07-07

## What I set out to learn

Understand how to deploy a secure web application in Azure using proper network isolation, controlled access, and Azure-managed services. Build a practical architecture combining VNets, Bastion, Firewall, and NAT rules.

## What I did

### Infrastructure Setup
- Created a **Resource Group** as the container for all resources
- Built an **Azure Virtual Network (VNet)** with multiple subnets:
  - Web app subnet (for the application server)
  - Bastion subnet (for secure management access)
  - Firewall subnet (for traffic routing and filtering)
- Configured **Azure Bastion** in its dedicated subnet for secure SSH access to private instances

### VM Deployment
- Provisioned an **Ubuntu virtual machine** in the private web app subnet
- Deployed the VM **without a public IP address** to keep it isolated from the internet
- VM remains unreachable directly from external networks

### Application Configuration
- Used **Bastion** to SSH into the private VM instance
- Updated the OS repository packages on the Ubuntu instance
- Installed **Nginx** web server
- Created and hosted a static **HTML** page

### Firewall & NAT Rules
- Configured **Network Address Translation (NAT)** rules in **Azure Firewall**
- Set up inbound rule to allow traffic from a specific external IP (my machine) on port 4,000
- Mapped port 4,000 to port 80 on the private Nginx server
- Firewall acts as a reverse proxy between internet and private application

### Verification
- Successfully accessed the application via browser using: `FirewallPublicIP:4000`
- Confirmed end-to-end connectivity through the secure architecture

## What I learned / key takeaways

- **Private subnets + Bastion = Security:** VMs with no public IPs are unreachable directly; Bastion provides controlled SSH access only through Azure Portal
- **Azure Firewall ≠ NSG:** Firewall is a managed layer 4/7 service that can do NAT, while NSGs are distributed rules at the NIC/subnet level
- **NAT rules enable selective exposure:** Firewall can translate external ports to internal ports, allowing granular access control without exposing internal infrastructure
- **Multi-subnet architecture matters:** Separating Bastion, Firewall, and application subnets is a security best practice (defense in depth)
- **Bastion eliminates jump boxes:** No need for public IPs or bastion hosts when using Azure Bastion — connect securely through the portal

## Resources

- Azure Virtual Network (VNet) documentation
- Azure Bastion — secure access to private instances
- Azure Firewall — managed firewall service and NAT rules
- Nginx web server documentation

## Next steps

Explore more advanced networking topics: User Defined Routes (UDRs), Application Gateway/Load Balancer for high availability, and integrating Azure DevOps for CI/CD into this secure architecture.
