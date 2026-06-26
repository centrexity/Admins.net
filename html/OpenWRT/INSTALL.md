# Admins.net OpenWRT Packages

## Modern OpenWRT (apk-tools v3, OpenWRT 23.05+)

### One-time key setup
```bash
wget -O /etc/apk/keys/admins.net-20260625150102.rsa.pub https://dl.admins.net/OpenWRT/x86_64/admins.net-20260625150102.rsa.pub
```

### Install
```bash
echo "https://dl.admins.net/OpenWRT" > /etc/apk/repositories.d/adminsnet.list
apk update
apk add admins-net
```

### Sideload
```bash
apk add --allow-untrusted /tmp/admins-net-0.1.7-r1-x86_64.apk
```

---

## Legacy OpenWRT (apk-tools v2, pre-23.05)

### One-time key setup
```bash
wget -O /etc/apk/keys/admins.net-20260625150102.rsa.pub https://dl.admins.net/OpenWRT/legacy/x86_64/admins.net-20260625150102.rsa.pub
```

### Install
```bash
echo "https://dl.admins.net/OpenWRT/legacy" > /etc/apk/repositories.d/adminsnet.list
apk update
apk add admins-net
```

### Sideload
```bash
apk add --allow-untrusted /tmp/admins-net-0.1.7-r1-x86_64.legacy.apk
```

---

## opkg (very old OpenWRT / LEDE)

```bash
echo "src/gz adminsnet https://dl.admins.net/OpenWRT" >> /etc/opkg/customfeeds.conf
opkg update
opkg install admins-net
```

---

## Service Control

```bash
/etc/init.d/admins.net start|stop|restart|status
/etc/init.d/admins.net enable
logread | grep Admins.net
```

Built: 1782515201 | Version: 0.1.7