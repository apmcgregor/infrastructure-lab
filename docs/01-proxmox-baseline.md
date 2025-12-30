# Module 01 – Proxmox Baseline

## Why Proxmox comes first

Before any automation, networking, or security work can happen, there needs to be
a stable place for it to live. In this lab, that foundation is a single Proxmox
host.

Proxmox is not treated as a cloud platform or a control plane in its own right.
It is treated as **boring, trusted infrastructure**—a substrate on which
everything else runs. The goal of this module is not to master Proxmox features, I've no doubt there's a course somewhere on that,
but to establish a predictable baseline that can support frequent rebuilds.

If the host itself is unstable or over-engineered, everything built on top of it
becomes harder to reason about.

---

## The role of the hypervisor in this lab

In cloud environments, the hypervisor layer is intentionally invisible. You do
not configure it per workload, and you rarely interact with it directly. This
lab mirrors that model.

The Proxmox host is:
- Trusted while running
- Managed infrequently
- Kept as simple as possible
- Rebooted when necessary without ceremony

All meaningful infrastructure decisions happen *above* this layer.

---

## Keep the baseline intentionally simple

This module emphasizes restraint.

At this stage:
- Storage should be straightforward
- Networking should be minimal
- Security should be adequate, not maximal
- Defaults are usually correct

Complexity introduced too early becomes legacy that must be supported later.

---

## Storage as a foundation, not a feature

Storage in this lab is treated as **capacity and reliability**, not as a place
to demonstrate advanced features.

The baseline assumptions are:
- The Proxmox OS lives on dedicated storage
- VM storage is separate from the OS
- Redundancy is preferred if available
- Encryption is deferred to the VM layer

This mirrors cloud platforms, where disk encryption and identity are handled per
workload rather than per hypervisor.

---

## Networking is plumbing, not architecture (yet)

At this stage, networking exists only to provide:
- Management access to the host
- Basic connectivity for VMs
- A path to automation tools

A single bridge connected to the physical network is sufficient.

Isolation, routing, firewalls, and segmentation are intentionally deferred until
later modules, once VM lifecycle management is reliable.

---

## What “done” looks like

A correct Proxmox baseline is unremarkable.

You should be able to:
- Reach the web interface reliably
- SSH to the host
- Reboot the host without surprises
- Create and delete test VMs manually (for now)

If your Proxmox setup feels exciting or clever, it is probably too complex for
this stage.

---

## What this module is *not* about

This module does **not** aim to:
- Harden Proxmox to production standards
- Use every ZFS feature
- Build complex networking
- Enable high availability
- Solve multi-node clustering

Those are valid topics—but not yet.

---

## Why this simplicity matters later

Every later module depends on the assumptions established here.

If:
- The host is stable
- Storage behavior is predictable
- Networking is understandable

Then failures higher up the stack are easier to diagnose and recover from.

This lab optimizes for **clarity under failure**, not maximum performance or
security on day one.

---

## Operational mindset

You should treat the Proxmox host as:
- Important, but not fragile
- Stable, but not sacred
- A tool, not a project

If you find yourself tuning or perfecting the host instead of building on top of
it, step back. That instinct will be challenged repeatedly in later modules.

---

## What comes next

In the next module, you will stop using the Proxmox UI to create machines and
introduce Terraform as the authoritative source of truth for VM lifecycle.

Once that shift happens, the role of the Proxmox UI changes—from control plane to
observability tool.

Before moving on, make sure you understand:
- Why the hypervisor is intentionally boring
- Why complexity is deferred
- Why VM rebuildability matters more than host tuning

These assumptions will not be revisited later.
