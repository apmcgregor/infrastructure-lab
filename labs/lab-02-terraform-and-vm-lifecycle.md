# Lab 02 – Terraform Provider & First VM

## Purpose of this lab

This lab introduces Terraform as the **authoritative control plane** for virtual
machines. The goal is to move VM creation out of the Proxmox UI and into code,
while keeping the system simple enough to understand what is happening.

By the end of this lab, you should be able to:
- Run Terraform **from your local workstation**
- Authenticate Terraform **to a remote Proxmox host**
- Create a VM without using the Proxmox UI
- Destroy and recreate that VM confidently
- Understand where configuration lives and where it does not

This lab is deliberately explicit about *where commands are run*.

---

## Execution context (read this first)

Throughout this lab, there are **three distinct systems** involved:

### 1. Your local workstation (primary workspace)
This is where you will:
- Edit files
- Run Terraform commands
- Commit changes to Git

Examples:
- Your laptop
- Your desktop
- Any machine with Git and Terraform installed

Unless explicitly stated otherwise, **all commands in this lab are run on your
local workstation**.

---

### 2. The Proxmox host (remote infrastructure)
This is the machine running Proxmox.

You will:
- Log into the web UI to *observe* changes
- Occasionally SSH to it for setup tasks (called out explicitly)

You will **not**:
- Run Terraform here
- Manually create or edit VMs here

The Proxmox host is controlled remotely.

---

### 3. The virtual machine (created later)
This VM will be:
- Created by Terraform
- Disposable
- Not interacted with directly yet

In this lab, you do not SSH into the VM.

---

If you are ever unsure where a command runs:
- **Default to your local workstation**
- Only use the Proxmox host when explicitly instructed

---

## Preconditions

Before starting, confirm:

### On your local workstation
- [ ] Git is installed
- [ ] Terraform is installed (`terraform version` works)
- [ ] You can reach the Proxmox web UI in a browser

### On the Proxmox host
- [ ] Proxmox is installed and stable
- [ ] You can log into the web UI
- [ ] You can SSH to the host as root or an admin user

Do not proceed if any of these are missing.

---

## What you are building (scope)

In this lab you will create:
- A Terraform workspace on your **local workstation**
- A Proxmox provider configuration
- One disposable VM on the **Proxmox host**

This VM will:
- Have minimal resources
- Use basic networking
- Exist only as a lifecycle test

---

## Exercise 1 – Create the Terraform workspace  
**(Local workstation)**

**Goal:** Establish Terraform as a first-class tool in the repo.

### Steps
- Create a `terraform/` directory in the repo
- Inside it, create:
  - `providers.tf`
  - `main.tf`
  - `variables.tf` (empty is fine for now)

- Ensure `.gitignore` includes:
  - `.terraform/`
  - `*.tfstate`
  - `*.tfstate.backup`

### Checklist
- [ ] Files exist locally
- [ ] Terraform files are tracked by Git
- [ ] State files are ignored

**Outcome:**  
You have a clean Terraform workspace on your local machine.

---

## Exercise 2 – Create a Proxmox API user  
**(Proxmox host)**

**Goal:** Allow Terraform to authenticate securely.

This step is performed **once**, directly against Proxmox.

### Steps
- Log into the Proxmox web UI
- Create a dedicated API user (e.g. `terraform@pam`)
- Generate an API token for that user
- Assign minimal permissions required to manage VMs

### Important
- Do **not** reuse your personal account
- Do **not** commit tokens to Git

Store credentials securely (environment variables or a local secrets file).

### Checklist
- [ ] API user exists
- [ ] API token generated
- [ ] Permissions are limited
- [ ] Credentials are stored outside the repo

---

## Exercise 3 – Configure the Terraform provider  
**(Local workstation)**

**Goal:** Allow Terraform to talk to Proxmox remotely.

### Steps
- Edit `providers.tf`
- Configure the Proxmox provider with:
  - Proxmox API URL
  - API user
  - API token
- Use variables or environment variables for secrets

### Validation
Run the following **locally**:

```bash
terraform init
```

### Checklist

- [ ] Provider plugins download successfully
- [ ] No authentication errors
- [ ] No secrets are hard-coded in Terraform files

**Outcome:**
Terraform can communicate with Proxmox.

### Exercise 4 – Verify access without creating resources

(Local workstation)

Goal: Confirm Terraform works before modifying infrastructure.
Steps

Run:

terraform plan

Expected result

    No changes

    No errors

    No resources created

Checklist

Plan completes successfully

    Terraform state is empty

Exercise 5 – Declare your first VM

(Local workstation)

Goal: Define a VM entirely in code.
Steps

    Edit main.tf

    Add a VM resource using:

        An existing cloud image or template

        1–2 CPU cores

        Minimal RAM

        One network interface

    Do not make any changes in the Proxmox UI

Validation

Run:

terraform plan

Read the output carefully.
Checklist

Terraform plans to create exactly one VM

    No unexpected resources appear

Exercise 6 – Apply and observe

(Local workstation + Proxmox UI)

Goal: Trust automation and observe externally.
Steps

    Run terraform apply locally

    Open the Proxmox web UI

    Watch the VM appear

Rules

    Do not edit the VM

    Do not fix issues manually

    Observe only

Checklist

VM appears in Proxmox

    Terraform apply completes successfully

Exercise 7 – Destroy without hesitation

(Local workstation)

Goal: Normalize destruction.
Steps

Run:

terraform destroy

Confirm when prompted.
Checklist

VM disappears from Proxmox

    No manual cleanup required

If this feels uncomfortable, pause and reflect.
Failure scenarios (intentional exercises)

These failures should be triggered on purpose.
Failure 1 – Authentication failure

    Invalidate the API token

    Run terraform plan

    Observe the error

    Restore valid credentials

Lesson:
Terraform failures are early and explicit.
Failure 2 – Configuration drift

    Create a VM with Terraform

    Modify it manually in the Proxmox UI

    Run terraform plan locally

Lesson:
Manual changes are visible and temporary.
Failure 3 – State mismatch

    Create a VM

    Delete it manually in Proxmox

    Run terraform plan

Lesson:
Terraform reconciles intent, not reality.
Failure 4 – Bad configuration

    Intentionally misconfigure the VM resource

    Apply the change

    Observe failure

    Fix the configuration

    Destroy and recreate the VM

Lesson:
Rebuilds are faster and safer than debugging snowflakes.
Lab 02 – Completion criteria

You have completed this lab if:

Terraform runs from your local workstation

Proxmox is controlled remotely

VMs exist only when Terraform declares them

You destroyed at least one VM

    You experienced and recovered from a failure

If a VM exists that Terraform does not know about, this lab is not complete.
What comes next

In Lab 03, you will explore VM networking basics: bridges, interfaces, and
how traffic flows between VMs and the host.

Terraform remains the control plane.
The Proxmox UI remains an observation tool.

If that separation is clear, you are ready to continue.