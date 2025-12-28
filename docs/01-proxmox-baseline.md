# Proxmox Baseline

## Storage layout

- 2×500GB HDD → ZFS mirror → Proxmox OS
- NVMe:
  - ZFS mirror → management VMs
  - LVM-thin → lab / disposable VMs

## What is NOT encrypted

- Proxmox OS
- Hypervisor storage pools

## Why

- Host must boot unattended
- Encryption is enforced at VM level
