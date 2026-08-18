# Deployment Notes

This document records the main implementation stages without exposing credentials or secret files.

## Stage 1 — Raspberry Pi

1. Install Raspberry Pi OS Lite 64-bit.
2. Configure hostname, user, Wi-Fi, and SSH.
3. Update the operating system.

## Stage 2 — OpenMediaVault

Install OpenMediaVault on Raspberry Pi OS Lite and access its web interface.

Configure:

- storage
- shared folders
- users
- permissions

## Stage 3 — LUKS

1. Prepare an empty storage drive.
2. Create a LUKS-encrypted volume.
3. Unlock the volume.
4. Create an EXT4 filesystem.
5. Mount the filesystem.
6. Create the NAS shared folder.

**Important:** Losing the LUKS passphrase can make the encrypted data unrecoverable.

## Stage 4 — FileBrowser

Configure FileBrowser to use the encrypted shared folder.

The project used port `3670` for the local FileBrowser service.

## Stage 5 — Cloudflare

1. Register/use a domain.
2. Delegate DNS to Cloudflare.
3. Install `cloudflared`.
4. Authenticate the Raspberry Pi.
5. Create a tunnel.
6. Route the domain to the tunnel.
7. Configure ingress rules.

## Stage 6 — Jellyfin

Run Jellyfin as a Podman container.

The project used port `8096` and mounted the media directory as read-only for Jellyfin.

## Stage 7 — Verification

Verify the complete lifecycle:

```text
Upload file
    ↓
FileBrowser
    ↓
Encrypted storage
    ↓
Jellyfin media scan
    ↓
Media playback
```

## Troubleshooting Notes

Observed issues included network loss after OMV installation, Wi-Fi conflicts, DNS propagation delays, SSL configuration problems, and Cloudflare access/WAF rules blocking requests.

Temporary USB tethering was used during network troubleshooting.
