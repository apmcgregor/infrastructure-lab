# VM-Level Disk Encryption

Each VM encrypts its own root disk on first boot.

## Mechanism

- LUKS2
- Clevis
- Tang (network-bound unlock)

## Properties

- Each VM has a unique disk key
- No human interaction
- Fully unattended boot
- Rebuild = new cryptographic identity

This mirrors cloud provider disk encryption models.
