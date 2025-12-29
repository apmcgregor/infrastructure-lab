# cloud-init as the Control Plane

cloud-init is treated as the primary mechanism for:

- User creation
- SSH access
- Package installation
- Disk encryption
- Identity enrollment

VMs are never configured manually after boot.

cloud-init files live in Git and are synced to Proxmox
as snippets.
