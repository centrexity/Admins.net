# Admins.net OpenWRT Packages

Single URL for both modern and legacy OpenWRT:

```
https://dl.admins.net/OpenWRT
```

`apk` automatically appends `/x86_64/` when resolving the index.

---

## Modern OpenWRT (apk)

### One-time key setup (per router)

```bash
wget -O /etc/apk/keys/admins.net-20260625150102.rsa.pub \
     https://dl.admins.net/OpenWRT/x86_64/admins.net-20260625150102.rsa.pub
```

### Install

```bash
echo "https://dl.admins.net/OpenWRT" > /etc/apk/repositories.d/adminsnet.list
apk update
apk add admins-net
```

### Sideload (no repo)

```bash
scp x86_64/admins-net-0.1.7-r1-x86_64.apk root@router:/tmp/
apk add --allow-untrusted /tmp/admins-net-0.1.7-r1-x86_64.apk
/etc/init.d/admins.net enable && /etc/init.d/admins.net start
```

---

## Legacy OpenWRT (opkg)

```bash
echo "src/gz adminsnet https://dl.admins.net/OpenWRT" >> /etc/opkg/customfeeds.conf
opkg update
opkg install admins-net
```

### Sideload

```bash
scp admins-net_0.1.7_x86_64.ipk root@router:/tmp/
opkg install /tmp/admins-net_0.1.7_x86_64.ipk
```

---

## Service Control

```bash
/etc/init.d/admins.net start|stop|restart|status
/etc/init.d/admins.net enable
logread | grep Admins.net
```

---

Built: 1782423479 | Version: 0.1.7