# Core Principles

Before touching any tools, this lab follows these rules:

1. **Everything is disposable**
   If a VM breaks, it is destroyed and rebuilt.

2. **Humans authenticate, machines authenticate**
   - Humans: SSH certificates
   - Machines: unique identities

3. **Encryption is per-VM, not per-host**
   This mirrors cloud provider behavior.

4. **No manual configuration drift**
   If it isn’t in Git, it doesn’t exist.

5. **Boot must be unattended**
   Power loss should not require human interaction.

Threat model:
- Protect against disk theft
- Assume host compromise = game over (same as cloud)
