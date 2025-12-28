Working Document

# infrastructure-lab

**A hands-on lab for building, securing, and rebuilding cloud-like infrastructure.**

This repository is an opinionated learning lab focused on modern infrastructure
practice rather than long-lived services. The goal is to explore how real-world
platform and cloud teams design systems that are automated, disposable, secure,
and observable — using a single physical machine as the foundation.

The lab uses Proxmox as a hypervisor, Terraform for lifecycle management, and
cloud-init as the machine control plane. From there, it layers in networking and
routing, per-VM disk encryption, centralized identity, certificate-based access,
monitoring, and schedulers such as Nomad or Kubernetes.

Everything is defined in Git. Machines are expected to be rebuilt. Failure is a
feature. The focus is on understanding *why* systems are designed the way they
are, not just *how* to make them run.

# Cloud Lab – Infrastructure Engineering on a Single Machine

This repository contains a complete, rebuildable infrastructure lab designed
to mirror modern cloud platforms using a single Proxmox host.

The goal is not to run services forever, but to **practice designing,
automating, breaking, and rebuilding infrastructure** the way cloud providers
and platform teams do.

## What this lab covers

- Proxmox as a hypervisor
- Terraform-driven VM lifecycle
- cloud-init as the machine control plane
- Per-VM disk encryption (Tang + Clevis)
- Network isolation, routing, VPNs
- Central identity with FreeIPA
- SSH certificates (no authorized_keys sprawl)
- Monitoring with Prometheus and Grafana
- Disposable workloads (Nomad / Kubernetes / Slurm)

Module 0 – Principles & Threat Model
Module 1 – Base Platform (Proxmox + Storage)
Module 2 – Networking & Routing
Module 3 – Infrastructure as Code (Terraform)
Module 4 – Cloud-Init as the Control Plane
Module 5 – VM-level Encryption (Tang + Clevis)
Module 6 – Identity & Access (FreeIPA + SSH certs)
Module 7 – Monitoring & Observability
Module 8 – Workload Platforms (Nomad / k8s / Slurm)
Module 9 – Rebuilds, Rotation, and Failure

## Design principles

- Rebuild instead of repair
- Automation first
- No snowflake machines
- Per-VM identity and encryption
- Cloud-like trust boundaries

This is not a homelab tutorial. It is a **platform engineering lab**.

## Who this is for

This lab is for people who want hands-on experience with infrastructure concepts
such as automation, identity, encryption, and failure handling.

You will get the most out of this if you:
- Are comfortable with Linux basics
- Want to learn Terraform and cloud-init in practice
- Are curious how cloud platforms work under the hood
- Prefer rebuilding systems over fixing snowflakes

This is not a turnkey homelab guide, and it is not focused on running production
services at home.

## License

Code (Terraform, scripts, configuration) is licensed under the MIT License.

Documentation, diagrams, and written material are licensed under
Creative Commons Attribution 4.0 (CC BY 4.0).

You are free to use, modify, and share this work, including commercially,
provided appropriate credit is given.