# pve-standalone-scripts

Standalone Bash tools for running Proxmox VE nodes: configuration backup for disaster recovery,
a host baseline (temp/cache layout, sysctl, journald, vzdump), and a quick diagnostic report.
Each tool is a single script with no dependencies beyond a stock Proxmox VE install.

| Tool | What it does |
|---|---|
| [`pve-backup`](pve-backup/) | Backs up the node's configuration (`/etc/pve`, network, storage, cluster files and the tools themselves) locally and to every matching storage, with retention per tier, a systemd timer and `--restore-plan` to find the newest usable copy. |
| [`pve-baseline`](pve-baseline/) | Applies a host baseline on a node with a fast local directory storage: temp and cache on that storage, vzdump `tmpdir`, conservative sysctl and journald limits, a swap-clean and a health-check timer. Reversible with `--uninstall`. |
| [`pve-diagnostic`](pve-diagnostic/) | Read-only report of the node's state (versions, storage, cluster, services, recent errors) into a log file. |

## Conventions

- Tools install to `/opt/pve-tools`, write logs to `/var/log/pve-tools` and keep state in `/var/lib/pve-tools`.
- Everything site-specific (retention, schedule, which storages to use) lives in an `.env` file next to the
  tool, never in the script. Copy the `*.env.example` and adjust it.
- Storage tiers are chosen by **storage ID**: a storage whose ID contains `FAST`, `BACKUP` or `OFFSITE` is
  used as that tier (`pve-baseline` uses the local directory storage whose ID contains `FAST`). Name your
  storage IDs accordingly, or disable a tier in the `.env`.
- Run a script without arguments to see its options. They are meant to be run as root on a Proxmox VE node.

## Status

Used in production on Proxmox VE 8 and 9 nodes. Test on a non-critical node first.

## Contact

Questions, ideas or collaboration: **[LinkedIn](https://www.linkedin.com/in/yrbusiness)**.
Bugs and improvements: GitHub issues and pull requests are welcome.

## License

MIT -- see [LICENSE](LICENSE).
