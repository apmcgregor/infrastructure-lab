# Module 00 – Principles & Threat Model

## Why this lab exists

This lab is not about running services at home, building a homelab dashboard, or
keeping systems alive indefinitely. It exists to practice **modern infrastructure
thinking**: how cloud and platform teams design systems that can be automated,
rebuilt, secured, and observed.

Everything that follows is shaped by one core idea:

> **Infrastructure should be disposable, reproducible, and boring to operate.**

If something breaks, the correct response is not to log in and fix it by hand, but
to understand *why it broke*, encode the fix in automation, and rebuild.

---

## Guiding principles

These principles apply to every module and every lab exercise in this repository.

### 1. Rebuild instead of repair

Manual fixes create snowflakes. Snowflakes don’t scale.

In this lab:
- Virtual machines are expected to be destroyed and recreated
- Configuration lives in Git, not on the machine
- Recovery means “re-run Terraform”, not “SSH and debug”

If a system cannot be rebuilt cleanly, it is considered broken—even if it appears
to work.

---

### 2. Automation first

Every system in this lab should be created by automation before it is ever used.

That means:
- Terraform defines *what exists*
- cloud-init defines *how machines configure themselves*
- Scripts are helpers, not sources of truth

Manual steps are acceptable only when explicitly called out as learning exercises,
and even then they should be temporary.

---

### 3. Infrastructure is cattle, not pets

Machines are not special. Data is.

In practice:
- VM names are descriptive, not sentimental
- Recreating a VM is normal
- Unique identity is generated at provisioning time
- Long-lived state is minimized

If losing a VM feels scary, it’s a signal that too much responsibility has been
placed on it.

---

### 4. Identity and trust are explicit

Trust is never assumed implicitly.

This lab treats:
- Humans and machines as different identities
- Authentication as a first-class concern
- Certificates as preferable to static secrets
- Central identity as more important than local users

Access is granted deliberately, expires where possible, and can be revoked
centrally.

---

### 5. Encryption is the default, but practical

Encryption is used to protect against realistic threats, not to chase perfect
security.

In this lab:
- Disk encryption protects against disk theft and offline access
- Encryption is applied at the VM level to mirror cloud behavior
- Boot is unattended and automated
- Human interaction is not required after power loss

Security mechanisms that prevent recovery or learning are avoided.

---

## Threat model (what we care about)

This lab uses a **cloud-style threat model**, not a high-assurance or adversarial
one.

### We assume:
- The physical host is trusted while running
- The hypervisor is trusted
- The management network is controlled

### We protect against:
- Disk theft
- Offline access to VM data
- Credential sprawl
- Long-lived static secrets
- Accidental exposure due to misconfiguration

### We explicitly do *not* protect against:
- A fully compromised host
- An attacker with root access to a running system
- Nation-state or forensic-level adversaries

This is intentional and mirrors how most public cloud platforms define their
responsibility boundaries.

---

## What “cloud-like” means in this lab

Throughout this repository, “cloud-like” does **not** mean:
- Running Kubernetes everywhere
- Recreating AWS services exactly
- Hiding complexity behind GUIs

Instead, it means:
- Infrastructure defined as code
- Machines boot unattended
- Identity is centralized
- Encryption is automatic
- Rebuilds are expected
- Failure is survivable

The goal is to understand the *patterns*, not to clone a specific provider.

---

## How to use this lab

You are expected to:
- Read the conceptual documentation before doing labs
- Break things intentionally
- Rebuild often
- Modify examples to test your understanding

You are *not* expected to:
- Follow instructions blindly
- Keep everything running forever
- Avoid mistakes

Mistakes are part of the learning process. If you never break anything, you are
not using the lab correctly.

---

## What comes next

In the next module, we will establish a minimal Proxmox baseline. This gives you
a stable foundation on which everything else is built—but it is intentionally
simple and unoptimized.

Complexity will be added gradually, and always for a reason.

Before moving on, make sure you understand:
- Why rebuilds are preferred to repairs
- Why automation matters more than tools
- Why the threat model is intentionally limited

These ideas will come up again and again.
