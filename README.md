Working Document

# infrastructure-lab

**A hands-on lab for building, securing, and rebuilding cloud-like infrastructure.**

This repository is a learning lab focused on modern infrastructure
practice rather than long-lived services. The goal is to explore how real-world
platform and cloud teams design systems that are automated, disposable, secure,
and observable — using a single physical machine as the foundation.

The lab uses Proxmox as a hypervisor, Terraform for lifecycle management, and
cloud-init as the machine control plane. From there, it layers in networking and
routing, per-VM disk encryption, centralized identity, certificate-based access,
monitoring, and perhaps schedulers such as Nomad or Kubernetes if time allows.

Everything is defined in Git. Machines are expected to be rebuilt. Failure is a
feature. The focus is on understanding *why* systems are designed the way they
are, not just *how* to make them run.

# Cloud Lab – Infrastructure Engineering on a Single Machine

This repository contains a complete, rebuildable infrastructure lab designed
to mirror modern cloud platforms using a single Proxmox host instead of going out to the cloud.

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

## Module list
It's broken down into modules.  The modules are designed to be worked on in order.  Previous modules provide the base for the new module.

- Module 0 – Principles & Threat Model
- Module 1 – Proxmox Baseline
- Module 2 – Terraform & VM Lifecycle
- Module 3 – VM Networking Basics
- Module 4 – Network Architecture & Isolation
- Module 5 – cloud-init as Control Plane
- Module 6 – VM-Level Encryption (Tang + Clevis)
- Module 7 – Identity & SSH Certificates
- Module 8 – Monitoring & Observability
- Module 9 – Workload Platforms
- Module 10 – Operations & Failure


## Design principles

- Rebuild instead of repair - there's no editing a VM.  We will edit the configuration in Git and rebuild the VM, rather than fix it.
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

The drive for me in writing this (with ChatGPT's help), is to cement my learning of these topics without breaking any production systems at work.

I've bought a workstation of Ebay with a high core count to make this possible.

## License

The code (Terraform, scripts, configuration) is licensed under the MIT License.

The documentation, diagrams, and written material are licensed under
Creative Commons Attribution 4.0 (CC BY 4.0).

You are free to use, modify, and share this work, including commercially,
provided appropriate credit is given.