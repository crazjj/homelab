# My homelab

> Notes and reduced examples from the Linux server I run at home.

My first self-hosting experiments ran on a Raspberry Pi. I tried Pi-hole,
PiVPN, Nextcloud and small Minecraft servers before moving to a dedicated mini
PC. For the current system I bought an Intel N150 barebone, added 32 GB of DDR4
memory and a 2 TB NVMe SSD, installed Fedora and gradually rebuilt the services
around Podman.

Most services are existing open-source applications rather than software I
wrote myself. My part is selecting, deploying, connecting, updating, backing
up and troubleshooting them. I also use the server for Gradle builds,
Minecraft infrastructure and experiments with development environments.

The files here are reconstructed examples, not exports from the live server. I
replaced real hostnames, addresses and credentials and added Gitleaks as a
second check. I still review every file before publishing it.

I kept most of my projects private for a long time. This homelab is the first
of several projects I am preparing for my dual-study applications.

## Current setup

| Area | Current state | What I have actually checked |
| --- | --- | --- |
| Host | Fedora, Btrfs and rootful Podman on the N150 system | The services run day to day; Btrfs is not treated as a backup. |
| Access | Zoraxy for selected web routes and WireGuard for private administration | The routes work, but I have not yet compared the complete public surface with an outside-in scan. |
| Development | OneDev mirrors selected repositories and packages Gradle artifacts | The current job compiles and packages with `-x test`; it is not a test-verified build. |
| Stateful services | Nextcloud, ArchiveBox and Minecraft data | I can operate and troubleshoot them, but I have not restored a complete service yet. |
| Backups | Hourly Borg archives through Vorta plus copies away from the host | One small local file restore worked; off-device and full-service recovery are still untested. |

Web applications are intended to enter through Zoraxy, Minecraft through
`mc-router`, and management through WireGuard. It is still one small home
server: there is no high availability, several checks are manual and important
recovery steps still need testing.

## What changed how I think about the server

At first, the Compose files felt like the main description of the system. While
setting up backups and moving services, I learned how much important state also
lives in mounted data, generated configuration, certificates and application
settings. A container that starts successfully can still be unusable or hard
to recover.

The three questions I now ask before keeping a service are:

1. Where does its state live?
2. How do I update and troubleshoot it?
3. What would I need to restore after a failure?

The small N150 system also makes me choose services with a real purpose. One
example is using it to download games overnight while my louder gaming PC stays
off, then transferring them over the local network.

## Examples

- [Minecraft routing and coordinated backups](examples/minecraft/README.md)
- [OneDev artifact packaging](examples/onedev/README.md)

## Notes

- [Architecture and security boundaries](docs/architecture-and-security.md)
- [Current service landscape](docs/service-landscape.md)
- [Operations, backups and recovery](docs/operations-and-recovery.md)
- [Why I chose Fedora over Bluefin](docs/decisions/001-fedora-over-bluefin.md)

Next I want to restore one complete service from an off-device Borg copy,
replace the broad Podman access used by the Minecraft auto-start mechanism and
automate restart and rollback of my Paper test server before connecting it to
OneDev.

Licensed under the [MIT License](LICENSE).
