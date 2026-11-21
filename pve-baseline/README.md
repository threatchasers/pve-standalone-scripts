# pve-baseline

Host baseline for a Proxmox VE node that has a fast local directory storage (ID containing `FAST`,
mounted at `/mnt/pve/<ID>`, ideally from `/etc/fstab`).

```bash
./pve-baseline --install      # copy to /opt/pve-tools, wrapper, timers
pve-baseline --run            # apply the baseline
pve-baseline --status
pve-baseline --health-check-only
pve-baseline --swap-clean-only
pve-baseline --uninstall      # remove what it added
```

What it applies: temp and cache directories on the fast storage, vzdump `tmpdir` and guest temp excludes in a
managed block of `/etc/vzdump.conf`, conservative `vm.*` sysctl values, journald size limits, a daily safe
swap-clean timer and a 6-hourly health-check timer. Every file it writes is named after the tool, so
`--uninstall` removes exactly that.
