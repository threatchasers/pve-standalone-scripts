# pve-backup

Disaster-recovery backup of a Proxmox VE node's configuration.

```bash
./pve-backup --install                 # copies itself to /opt/pve-tools, wrapper, service and timer
cp pve-backup.env.example /opt/pve-tools/pve-backup.env   # optional: edit retention, tiers, schedule
pve-backup --run                       # one backup now
pve-backup --status
pve-backup --restore-plan              # newest usable backup across all storages
pve-backup --uninstall
```

- Local copy: `/var/backups/pve-tools/nodes/<last3octets>/PVE-Backup/<timestamp>`.
- Remote copies go to every storage whose ID contains `FAST`, `BACKUP` or `OFFSITE`, each tier with its own
  retention (`*_KEEP`) and on/off switch (`ENABLE_*`) in the `.env`.
- Remote operations are time-bounded, so an unreachable NFS/SMB storage does not hang the run.

> **The backup contains secrets**: `/etc/shadow`, `/etc/ssh` host keys, `/root` and the cluster config.
> Only point it at storages you trust and protect them accordingly.
