# Admins.net OpenWRT Packages

This repo is structured so `apk` automatically looks in `x86_64/` when you point it at the root.

**Single recommended URL:**

```
https://dl.admins.net/OpenWRT
```

`apk` will automatically append `/x86_64/` when looking for the index and packages.

## Setup (Modern OpenWRT)

```bash
echo "https://dl.admins.net/OpenWRT" > /etc/apk/repositories.d/adminsnet.list
apk update
apk add admins-net
```

> **Note:** If you see "UNTRUSTED signature", either:
> - Run with `--allow-untrusted`, or
> - Set up signing keys (see section below)

## Setting up Signing Keys (Recommended)

The build script now automatically generates a signing key if one doesn't exist and includes the public key in this repository.

**On your build machine:**
- The script will create `~/.abuild/admins.net-*.rsa` if needed.
- It copies the `.rsa.pub` file into this repo folder.

**On each router (one time):**

```bash
# Download and install the public key
wget -O /etc/apk/keys/admins.net.rsa.pub \
     https://dl.admins.net/OpenWRT/admins.net-*.rsa.pub

# Or manually:
# scp admins.net-XXXX.rsa.pub root@router:/etc/apk/keys/
```

After installing the key, you can use clean commands:

```bash
apk update
apk add admins-net
```

## Setup (Legacy OpenWRT)

```bash
echo "src/gz adminsnet https://dl.admins.net/OpenWRT" >> /etc/opkg/customfeeds.conf
opkg update
opkg install admins-net
```

## One-shot Install

**Modern:**
```bash
scp x86_64/admins-net-0.1.7-r1-x86_64.apk root@router:/tmp/
apk add --allow-untrusted /tmp/admins-net-0.1.7-r1-x86_64.apk
/etc/init.d/admins.net enable && /etc/init.d/admins.net start
```

**Legacy:**
```bash
scp admins-net_0.1.7_x86_64.ipk root@router:/tmp/
opkg install /tmp/admins-net_0.1.7_x86_64.ipk
```

## Service Control
```bash
/etc/init.d/admins.net start|stop|restart|status|enable
logread | grep Admins.net
```

Built: 1782353441 | Version: 0.1.7