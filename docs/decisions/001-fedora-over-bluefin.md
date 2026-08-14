# Why I chose Fedora over Bluefin

Before installing the homelab, I also considered Bluefin. Its image-based
updates and rollback are attractive for a workstation that should need little
maintenance. I chose regular Fedora because maintaining the host is part of
what I want to learn on this machine.

The N150 hardware benefits from a current Linux kernel and container stack.
Fedora also lets me work directly with packages, systemd and Podman. Its short
release cycle means more upgrade work, but that is a trade-off I accepted rather
than something I wanted the system to hide from me.

The installation uses Btrfs for the root filesystem and service-data
subvolumes. Checksumming, compression and snapshots are useful on a small
single-disk system, but they do not provide disk redundancy and I do not count
them as a backup. Recovery still depends on Borg and copies away from the host.

For a workstation I might choose Bluefin for rollback and lower maintenance.
For this server I wanted to work directly with the host, including the parts
that occasionally need troubleshooting.

## References

- [Fedora release life cycle](https://fedoraproject.org/wiki/Fedora_Release_Life_Cycle)
- [Btrfs in Fedora](https://fedoraproject.org/wiki/Btrfs)
- [Bluefin introduction](https://docs.projectbluefin.io/introduction/)
