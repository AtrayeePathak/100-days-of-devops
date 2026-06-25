# Day 01 — Linux Fundamentals

**Date:** 2026-06-26

## What I set out to learn

Refresh core Linux skills that come up constantly in DevOps work: file
permissions, process management, and systemd basics.

## What I did

- Reviewed `chmod`/`chown` and the numeric vs symbolic permission notation
- Used `ps`, `top`, and `kill` to inspect and manage running processes
- Wrote a tiny systemd unit file and enabled/started/stopped a service with it
- Practiced `journalctl` for reading service logs

## What I learned / key takeaways

- `chmod 750` = owner rwx, group r-x, others nothing — the numeric system
  finally clicked once I mapped it to binary (rwx = 4+2+1)
- `systemctl status <service>` plus `journalctl -u <service> -f` is the
  combo I'll reach for whenever a service "isn't working"
- Zombie vs orphan processes are different things — zombies have exited but
  still have an entry in the process table until the parent reaps them

## Resources

- `man systemd.unit`
- Linux Journey (permissions section)

## Next steps

Look at `ulimit` and basic resource constraints — relevant before jumping
into cgroups/containers next.
