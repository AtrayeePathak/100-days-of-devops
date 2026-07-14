# Day 07 — Deploying an Application Behind Azure Firewall

**Date:** 2026-07-12

## What I set out to learn

Apply the networking concepts from earlier days in a practical hands-on project: expose an application securely using Azure networking services.

## What I did

- Reviewed the architecture pattern of a private app hosted in a backend subnet
- Looked at how Azure Bastion can be used for secure access to private resources
- Revisited the idea of using a firewall as the public entry point for a private service
- Connected the day 02 notes with the broader design pattern from the Azure zero-to-hero course

## What I learned / key takeaways

- Private workloads do not need public IPs to be usable behind a controlled access path
- Bastion is a safer way to manage private VMs than exposing SSH directly
- Firewalls and NAT rules allow selective exposure of internal services without opening the whole network
- A practical project makes the networking concepts feel much more real than reading them alone

## Resources

- Azure Bastion documentation
- Azure Firewall NAT rules documentation
- Azure networking project notes from previous days

## Next steps

Try building a more complete architecture with a web tier, a backend tier, and a controlled public access layer.
