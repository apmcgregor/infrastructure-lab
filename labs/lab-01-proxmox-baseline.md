# Lab 01 – Proxmox Baseline

## Purpose of this lab

This lab establishes the **single physical foundation** for everything that
follows. The goal is not to tune Proxmox perfectly, but to create a **stable,
boring baseline** that can host rebuildable infrastructure.

At the end of this lab you should have:
- A working Proxmox installation
- Reliable remote access
- A simple, understandable storage layout
- A baseline network that is intentionally minimal

You should **not** attempt to optimize performance, security, or isolation yet.
Those will come later.

---

## Minimum system requirements (good guesses)

This lab is intentionally realistic. You do *not* need enterprise hardware, but
you do need enough headroom to rebuild systems frequently.

### Absolute minimum (will work, but tight)

- **CPU:** 8 cores (logical cores are fine)
- **RAM:** 32 GB
- **Storage:**
  - 1 × SSD (≥ 240 GB) for Proxmox OS
  - 1 × SSD or NVMe for VM storage
- **Networking:** 1 × 1 GbE NIC

This is enough to complete the labs, but you will need to be conservative with
VM sizes.

---

### Recommended minimum (comfortable learning)

- **CPU:** 12–16 cores
- **RAM:** 64 GB
- **Storage:**
  - 2 × SSDs (mirrored) for Proxmox OS
  - 1–2 × NVMe drives for VM storage
- **Networking:** 1–10 GbE NIC

This allows:
- Multiple concurrent VMs
- Monitoring stack
- Identity services
- Rebuilds without constant resource pressure

---

### Notes on hardware choices

- **ECC memory** is nice to have, not required
- **Consumer CPUs** are perfectly acceptable
- **Older enterprise hardware** is fine if power/noise are acceptable
- **TPM is not required** for this lab

If your system roughly meets the recommended minimum, it is sufficient.

>20251229 - On a personal note I found a good workstation on eBay for 249GBP with 128GB RAM and 2 x Xeon E5-2680

---

## Checklist: hardware readiness

Before installing anything, confirm the following:

### CPU & memory
- [ ] At least 8 logical CPU cores available
- [ ] At least 32 GB RAM installed
- [ ] Hardware virtualization enabled in BIOS (VT-x / AMD-V)
- [ ] IOMMU support is optional, not required yet

### Storage
- [ ] Dedicated disk(s) for Proxmox OS
- [ ] Separate disk(s) for VM storage (SSD or NVMe)
- [ ] You are comfortable wiping these disks

### Networking
- [ ] At least one NIC connected to your LAN
- [ ] DHCP available on your LAN
- [ ] You understand this is *temporary* exposure to your home network

### Operational mindset
- [ ] You are okay reinstalling Proxmox if needed
- [ ] You are not storing irreplaceable data on this system
- [ ] You accept that this machine may be rebooted frequently

If any of these are uncomfortable, pause here and reconsider.

---

## Installation goals (what “done” looks like)

You do **not** need a perfect setup. You need a predictable one.

### Proxmox installation
- [ ] Proxmox installed from official ISO
- [ ] Latest stable release
- [ ] Root password set securely
- [ ] Email configured (optional)

### Storage layout (baseline)

Recommended baseline:
- **Proxmox OS:** ZFS mirror if you have two disks, otherwise single disk
- **VM storage:** simple ZFS pool or LVM-thin

At this stage:
- ❌ No encryption required
- ❌ No special tuning
- ❌ No Ceph

You can revisit storage later.

---

### Networking (keep it boring)

- [ ] Default bridge (`vmbr0`) exists
- [ ] Bridge is attached to physical NIC
- [ ] Proxmox host has a stable IP
- [ ] Web UI reachable from your workstation

Do **not**:
- Create VLANs yet
- Add firewall rules yet
- Attempt isolation yet

This is intentional.

---

## Checklist: post-install verification

Once Proxmox is installed, confirm:

- [ ] You can log in to the web UI
- [ ] You can SSH to the host
- [ ] The host survives a reboot
- [ ] Storage is visible and healthy
- [ ] No errors in the Proxmox dashboard

If something looks wrong, now is the time to reinstall.

---

## What you should *not* do yet

Resist the urge to:
- Harden the host
- Encrypt disks
- Build networks
- Create production-style layouts
- Tune ZFS aggressively

Those decisions depend on later modules.

---

## Why this lab is intentionally simple

In cloud environments:
- The hypervisor is boring
- The host is trusted
- Complexity lives *above* the base layer

This lab mirrors that model.

A simple, stable Proxmox host is a feature, not a limitation.

---

## Lab 01 – Completion criteria

You have completed this lab if:
- Proxmox is installed and reachable
- You understand your hardware limits
- You have a simple storage layout
- You are ready to destroy and recreate VMs freely

You should feel slightly underwhelmed. That’s correct.

---

Everything from this point forward should be rebuildable.
