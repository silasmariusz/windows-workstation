# Asuswrt-Merlin firmware

[Asuswrt-Merlin Changelog](http://asuswrt.lostrealm.ca/changelog)

### Router Login Name

Non-root and non-admin.

### WAN

(PPPoE) User Name, Password

#### Port Forwarding

- tavsegitseg 5500/tcp
- RDP 3389/tcp
- HTTP/lakas  80/tcp
- HTTPS/lakas 443/tcp

### Wireless

SSID/WPA2-PSK AES

### Firmware

[check firmware version](https://www.mediafire.com/folder/bkfq2a6aebq68//Asuswrt-Merlin#yvgnw5wo8wrco)

### USB disk

Enable scheduled disk scan.

### LAN

Router LAN IP 192.168.13.254
LAN IP range 129.168.13.1 - 129.168.13.31

### NTP

NTP servers: hu.pool.ntp.org

### SSH

SSH public key

### DDNS

egry.no-ip.com

### IPv6 tunnel

SixXS

- Native/PPP
- DNS 2001:4860:4860::8888 2001:4860:4860::8844

### Backup

```bash
#!/bin/sh

opkg update
opkg upgrade

# backup items: settings, jffs, root files, USB drive

USB_ROOT="/tmp/mnt/optware"

[ -d "${USB_ROOT}/backup/" ] || exit 1
cd "${USB_ROOT}/backup/"

nvram save "Setting_$(nvram get productid).CFG" || exit 1
echo -------------------------------

tar cf jffs-bck.tar /jffs/ || exit 1
echo -------------------------------

tar cf root-bck.tar ../root/ || exit 1
echo -------------------------------

# USB drive backup
echo "listen: nc -l -p 1123 | gzip -9 > /opt/router-bck/router.tar.gz"
read
tar cv "$USB_ROOT" | nc szerver4. 1123 || exit 1
echo -------------------------------
```
