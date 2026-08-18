# Security Model

## 1. LUKS Encryption

LUKS protects data stored on the physical drive. The encrypted storage must be unlocked before the filesystem and applications can use it.

**Threat addressed:** physical theft or unauthorized access to the storage device.

## 2. Cloudflare Tunnel

The Raspberry Pi establishes an outbound tunnel to Cloudflare instead of requiring traditional inbound router port forwarding.

**Threat reduced:** direct exposure of home services through forwarded router ports.

## 3. RBAC

Two project users were configured:

- `public_user`: read-only
- `private_user`: read/write

This follows the principle of least privilege.

## 4. HTTPS

Remote access uses HTTPS through the Cloudflare endpoint.

## 5. Container Isolation

FileBrowser and Jellyfin are deployed using Podman containers, separating application processes from the host environment.

## Important Limitation

LUKS encryption protects data when the storage is locked. Once the drive is unlocked and the service is running, application-level authentication and authorization are still required.
