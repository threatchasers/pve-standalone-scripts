# pve-diagnostic

Read-only diagnostic of a Proxmox VE 8/9 node. Checks services first, then digs into whatever failed,
and writes the report to `/var/log/pve-tools` (last 3 kept).

```bash
./pve-diagnostic.sh                 # last 2 hours
./pve-diagnostic.sh "6 hours ago"   # custom window
```
