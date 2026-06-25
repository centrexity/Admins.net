# Admins.net – OpenWRT Packages

This directory contains pre-built packages for **OpenWRT**.

- **Recommended**: `admins-net-0.1.7-r1.apk` (for OpenWRT 25.12 and newer)
- **Legacy**: `admins-net_0.1.7_x86_64.ipk` (for older OpenWRT using opkg)

---

## Quick Install (Modern OpenWRT 25.12+)

```bash
# Copy the package to your router
scp admins-net-0.1.7-r1.apk root@192.168.1.1:/tmp/

# Install (unsigned / custom package)
apk add --allow-untrusted /tmp/admins-net-0.1.7-r1.apk

# Enable and start the service
/etc/init.d/admins.net enable
/etc/init.d/admins.net start

# Check status
/etc/init.d/admins.net status
logread | grep Admins.net
```

## Quick Install (Legacy OpenWRT)

```bash
scp admins-net_0.1.7_x86_64.ipk root@192.168.1.1:/tmp/
opkg install /tmp/admins-net_0.1.7_x86_64.ipk

/etc/init.d/admins.net enable
/etc/init.d/admins.net start
```

## Setting Up a Persistent Custom Repository

### For modern OpenWRT (apk)

1. Host this entire folder (`openwrt-repo/`) on a web server (nginx, Caddy, GitHub Pages, etc.).
2. On the router:

```bash
mkdir -p /etc/apk/repositories.d
echo "https://dl.admins.net/OpenWRT" > /etc/apk/repositories.d/adminsnet.list
apk update
apk add admins-net
```

### For legacy OpenWRT (opkg)

```bash
echo "src/gz adminsnet https://your.server.example.com/openwrt-repo" >> /etc/opkg/customfeeds.conf
opkg update
opkg install admins-net
```

## Service Management

| Command                        | Description                  |
|--------------------------------|------------------------------|
| `/etc/init.d/admins.net start`   | Start the service            |
| `/etc/init.d/admins.net stop`    | Stop the service             |
| `/etc/init.d/admins.net restart` | Restart                      |
| `/etc/init.d/admins.net status`  | Show status                  |
| `/etc/init.d/admins.net enable`  | Start on boot                |
| `logread \| grep Admins.net`             | View logs                    |

The service uses **procd** with automatic respawn on crash.

## Notes

- These packages are **unsigned**. Use `--allow-untrusted` (apk) or just `opkg install` for testing.
- For production repos you can sign the packages and generate `APKINDEX.tar.gz` using `apk index`.
- The binary is statically linked and should work on standard x86_64 OpenWRT builds.
- Built on: 1782348045  
  Version: 0.1.7

---

**Source / Support**: https://admins.net
