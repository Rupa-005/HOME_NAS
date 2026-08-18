# Architecture

## High-Level Flow

```text
Client Device
     |
     | HTTPS
     v
Cloudflare
     |
     | Cloudflare Tunnel
     v
Raspberry Pi
     |
     +--> FileBrowser :3670
     |
     +--> Jellyfin :8096
             |
             v
        Shared Media Storage
             |
             v
        LUKS-encrypted disk
```

## Hostname Routing

```text
<your-domain>
      |
      +--> http://localhost:3670
           FileBrowser

media.<your-domain>
      |
      +--> http://localhost:8096
           Jellyfin
```

The tunnel provides the public entry point while the applications remain local services on the Raspberry Pi.
