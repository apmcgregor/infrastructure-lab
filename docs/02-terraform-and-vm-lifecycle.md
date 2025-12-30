# Module 02 – Terraform & VM Lifecycle

## Why Terraform comes next

At this point, you have a working Proxmox host and a clear set of principles.
What you *do not* yet have is a reliable way to create and destroy machines
without touching the UI.

That is the gap Terraform fills.

Terraform is not introduced here because it is fashionable, but because it
forces a change in mindset:

> **If a machine cannot be created from code, it should not exist.**

From this module onward, virtual machines are not “created” — they are
**declared**. Their existence is the result of configuration, not clicks.

---

## What Terraform is responsible for in this lab

Terraform’s role is intentionally narrow.

In this lab, Terraform:
- Defines *which* machines exist
- Controls their lifecycle (create, destroy, rebuild)
- Attaches cloud-init metadata
- Connects machines to basic networking

Terraform does **not**:
- Configure software inside machines
- Replace cloud-init
- Manage secrets at runtime
- Fix broken systems

If Terraform is asked to do more than this, it is probably being misused.

---

## The VM lifecycle mindset

From this module onward, the default response to a broken VM is:

1. Identify what changed
2. Encode the change in configuration
3. Destroy the VM
4. Recreate it

Logging in to “just fix it” is explicitly discouraged.  We might need to, to debug or check logs, but the fix is applied to the configuration, not the VM.

This feels uncomfortable at first. That discomfort is part of the learning
process.

---

## Why networking is still simple

In this module, networking is intentionally boring.

- One network interface
- One bridge
- DHCP
- No isolation

This is not good architecture. It is a **scaffold**.

More networking will come later, once VM creation itself is predictable and
repeatable.

---

## State is not the enemy (but it is dangerous)

Terraform introduces the idea of **state**: a record of what Terraform believes
exists.

State is:
- Necessary
- Powerful
- Easy to misuse

In this lab:
- State is treated as disposable
- Losing state is annoying, not catastrophic
- Rebuilding is always preferred to repairing drift

You will learn to respect state without becoming afraid of it.

---

## What success looks like in this module

By the end of this module, you should be able to:

- Create a VM from Terraform alone
- Destroy that VM without hesitation
- Recreate it identically
- Make small changes and observe Terraform’s plan
- Avoid touching the Proxmox UI except for observation

If any VM exists that Terraform does not know about, that is a failure of
process — even if the VM “works”.

---

## Common mistakes (expected, not shameful)

It is normal in this module to:
- Feel slower than using the UI
- Break a VM and want to fix it manually
- Misconfigure cloud-init once or twice
- Forget that destroy is an option

The goal is not speed. The goal is **control**.

---

## How this module fits the bigger picture

Terraform is the backbone that everything else attaches to:
- Networking
- Identity
- Encryption
- Monitoring
- Workloads

Once machines are defined declaratively, higher-level systems become easier to
reason about — and easier to throw away.

---

## What comes next

In the next module, you will look at **basic VM networking**: not architecture,
but plumbing. You will learn just enough to understand how machines are
connected, without yet worrying about isolation or routing.

Before moving on, make sure you are comfortable with the idea that:
- VMs are disposable
- Terraform is authoritative
- Rebuilds are normal

If those ideas still feel strange, spend more time here. Everything that follows
assumes them.
