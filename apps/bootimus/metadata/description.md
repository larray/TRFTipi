---
name: Bootimus
short_desc: Self-contained PXE and HTTP boot server.
version: 0.1.80
---

<p align="center">
  <img src="metadata/bootimus_logo.png" alt="bootimus">
</p>

# Modern PXE/HTTP Boot Server

**A production-ready, self-contained PXE and HTTP boot server** written in Go with embedded iPXE bootloaders, SQLite/PostgreSQL support, and a full-featured web admin interface. Deploy in seconds with a single binary or Docker container.

# Once booted:
# Check logs for admin password
docker logs bootimus | grep "Password"

## Website live
### [https://bootimus.com/](https://bootimus.com/)

## There Be Dragons!

This is an early-stage work-in-progress project - there may be bugs. Please raise an issue for any unexpected behaviour you encounter.

### AI Disclosure

I've used Claude CLI to help with some parts of this project - mostly making the web UI pretty, as I'm NOT a frontend developer. I also used it to generate the docs, but I review them manually - no automatically-generated AI code goes into the project without review from myself.

## Features

- **Single binary, zero config**: Everything bundled - bootloaders, web UI, database. Just run it
- **Standalone PXE**: Built-in proxyDHCP responder lets Bootimus drive PXE on any LAN without touching the existing DHCP server
- **50+ distro support**: Automatic kernel/initrd extraction with a generic fallback scanner for unknown ISOs, plus OpenBSD and NetBSD netboot through their own loaders (new, feedback welcome)
- **Unattended Windows install** (opt-in): PXE-boot Windows 10/11 end-to-end — Bootimus hosts the install media over SMB and auto-launches `setup.exe`. Requires `samba` on the host (bundled in the Docker image)
- **Built-in diagnostic tools**: GParted, Clonezilla, Memtest86+, SystemRescue, ShredOS, Netboot.xyz - one-click download and enable from the admin UI
- **Custom tools**: Add your own PXE-bootable tools with configurable boot methods (kernel, chain, memdisk)
- **WinPE and rescue media**: Boot Strelec, Active@ Boot Disk and other wimboot-compatible ISOs, choosing which WIM to load
- **Checksums and update notices**: Downloads from the catalogue are verified against SHA-256 checksums, and images and tools show a badge when a newer release is available
- **Per-client access control**: Assign specific images per MAC address, toggle public image visibility per client
- **Deployment profiles**: Bundle an image, auto-install file, SAN target, bootloader set and a first-boot action, assign the bundle to clients or groups, and it is resolved at every boot
- **Auto-enrolment rules**: Match new machines on MAC prefix, manufacturer, product, serial, UUID or firmware and drop them into the right group and profile, named and static, on their first boot
- **Client auto-discovery**: Clients are automatically detected when they PXE boot, like DHCP leases - promote to static when ready
- **Next boot action**: Set a one-time boot image for a client with optional Wake-on-LAN - auto-clears after use
- **Disk capture and deploy**: Image a client's disk with the bundled Clonezilla and restore it to one client or a whole client group on their next PXE boot
- **iSCSI and AoE boot**: Point a client or group at a SAN target, with CHAP, and make it the default boot entry
- **Install completion tracking**: Kickstart, preseed, cloud-init and autounattend call back when an install finishes, so each client shows its install state and fires a webhook
- **BMC power control**: Power clients on, off or restart them over Redfish or Intel AMT, per client or in bulk across a client group
- **Remote console**: Open an Intel AMT Serial-over-LAN or IPMI console in the browser straight from the client page
- **Boot menu preview**: See the exact iPXE script any client would receive, without touching its state
- **PXE Debug page**: Every DHCP request the built-in proxyDHCP sees, with the decision taken, live in the admin UI
- **Hardware inventory**: Automatic collection of CPU, memory, manufacturer, serial number, and NIC info from PXE clients
- **JWT authentication**: Secure token-based auth with a dedicated login page, optional TOTP two-factor and lockout after repeated failed logins
- **API tokens**: Long-lived read-only or admin tokens for scripts and integrations, revocable at any time
- **Admin TLS**: Serve the admin interface over HTTPS with your own certificate or a generated self-signed one
- **LDAP/Active Directory**: Optional LDAP backend with group-based admin access - local accounts always work as fallback
- **OIDC single sign-on**: Sign in through Authentik, Keycloak, Microsoft Entra ID, Google or any OpenID Connect provider, with users created on first sign-in and admin rights mapped from groups or user lists
- **Read-only role**: Non-admin users can view clients, images and boot activity without being able to change anything or see BMC passwords
- **Audit log**: Every change made through the admin API is recorded with user, action and result, and can be forwarded as a webhook
- **Housekeeping**: Configurable retention for boot logs, inventory history, audit entries and stale discovered clients, with a data directory usage view
- **Backup and restore**: Download a backup of the database and settings, and restore one from the UI
- **Multi-site**: Read-only replicas at branch sites mirror a primary and boot local clients from local copies
- **Swappable bootloaders**: Ship with embedded iPXE, or bring your own custom bootloader sets
- **Raspberry Pi netboot**: Pi 3 and Pi 4 boards boot with no SD card — embedded UEFI firmware served over TFTP
- **Modern admin UI**: Sidebar navigation, consistent toolbars, real-time colour-coded logs, REST API with a generated OpenAPI document
- **Multi-database**: SQLite out of the box, PostgreSQL for production
- **Docker and bare metal**: Multi-arch images (amd64/arm64) or a single static binary
