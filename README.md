# Meshtastic OpenWRT Repo

Home to our APK and OPKG repositories for easily installing Meshtastic on OpenWRT-supported routers.

If you're looking for the package source code, check out [meshtastic/openwrt](https://github.com/meshtastic/openwrt).

## Supported OpenWRT versions
- `SNAPSHOT` (master branch)
- `24.10` (stable)

## How to use

This repository is currently hosted on [GitHub Pages](https://github.com). If you have problems accessing [this repo](https://openwrt.meshtastic.org) or access to GitHub [may be blocked](https://en.wikipedia.org/wiki/Censorship_of_GitHub) in your country, skip to the `Add repository to your OpenWrt device (jsDelivr)` sections. Both repositories use HTTPS protocol and require one of the SSL support packages to be installed on your router.

### OPKG
Used in stable versions of OpenWRT.

Supported versions:
- `24.10`

##### Add OPKG repository to your OpenWRT device (GitHub)

```sh
opkg update
opkg install wget-ssl
wget -O /etc/opkg/keys/1d36966d48075ff5 https://openwrt.meshtastic.org/meshtastic-ipk.pub
sed -i '/meshtastic/d' /etc/opkg/customfeeds.conf
ARCH=$( . /etc/openwrt_release; echo "$DISTRIB_ARCH" )
echo "src/gz meshtastic https://openwrt.meshtastic.org/openwrt-24.10/${ARCH}" >> /etc/opkg/customfeeds.conf
opkg update
```

##### Add OPKG repository to your OpenWRT device (jsDelivr)
Only use in regions where GitHub is blocked 🇨🇳

```sh
opkg update
opkg install wget-ssl
wget -O /etc/opkg/keys/1d36966d48075ff5 https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo/meshtastic-ipk.pub
sed -i '/meshtastic/d' /etc/opkg/customfeeds.conf
ARCH=$( . /etc/openwrt_release; echo "$DISTRIB_ARCH" )
echo "src/gz meshtastic https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo/openwrt-24.10/${ARCH}" >> /etc/opkg/customfeeds.conf
opkg update
```

Please note that there may be delay in [jsDelivr CDN](https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo) cache updates compared to [the repo at GitHub](https://openwrt.meshtastic.org) which may cause `opkg` to pull older files and/or complain about wrong signature.

---

### APK
Used in `SNAPSHOT` (master) builds. For stable OpenWRT versions see `OPKG` above.

##### Add APK repository to your OpenWRT device (GitHub)

```sh
echo "https://openwrt.meshtastic.org/main/$(cat /etc/apk/arch)/packages.adb" > /etc/apk/repositories.d/meshtastic.list
wget https://openwrt.meshtastic.org/meshtastic-apk.pem -O /etc/apk/keys/meshtastic-apk.pem
apk update
```

##### Add APK repository to your OpenWRT device (jsDelivr)
Only use in regions where GitHub is blocked 🇨🇳

```sh
echo "https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo/main/$(cat /etc/apk/arch)/packages.adb" > /etc/apk/repositories.d/meshtastic.list
wget https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo/meshtastic-apk.pem -O /etc/apk/keys/meshtastic-apk.pem
apk update
```

Please note that there may be delay in [jsDelivr CDN](https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo) cache updates compared to [the repo at GitHub](https://openwrt.meshtastic.org) which may cause `apk` to pull older files and/or complain about wrong signature.
