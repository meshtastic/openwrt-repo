# Meshtastic OpenWRT Repo

Home to our APK and OPKG repositories for easily installing Meshtastic on OpenWRT-supported routers.

If you're looking for the package source code, check out [meshtastic/openwrt](https://github.com/meshtastic/openwrt).

## Supported OpenWRT versions
- `SNAPSHOT` (master branch)
- `25.12` (stable)
- `24.10` (old-stable)
- `23.05` (old-stable)
- `22.03` (old-stable)

## How to use

This repository is currently hosted on [GitHub Pages](https://github.com). If you have problems accessing [this repo](https://openwrt.meshtastic.org) or access to GitHub [may be blocked](https://en.wikipedia.org/wiki/Censorship_of_GitHub) in your country, skip to the `Add repository to your OpenWrt device (jsDelivr)` sections. Both repositories use HTTPS protocol and require one of the SSL support packages to be installed on your router.

### APK
Used in the latest stable OpenWrt versions.

Supported versions:
- `25.12`

##### Add APK repository to your OpenWRT device (GitHub)

```sh
WRT_VER=$( . /etc/openwrt_release; echo "${DISTRIB_RELEASE%%-*}" | cut -d. -f1-2 )
echo "https://openwrt.meshtastic.org/${WRT_VER}/$(cat /etc/apk/arch)/packages.adb" > /etc/apk/repositories.d/meshtastic.list
wget https://openwrt.meshtastic.org/meshtastic-apk.pem -O /etc/apk/keys/meshtastic-apk.pem
apk update
```

##### Add APK repository to your OpenWRT device (jsDelivr)
Only use in regions where GitHub is blocked 🇨🇳

```sh
WRT_VER=$( . /etc/openwrt_release; echo "${DISTRIB_RELEASE%%-*}" | cut -d. -f1-2 )
echo "https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo/${WRT_VER}/$(cat /etc/apk/arch)/packages.adb" > /etc/apk/repositories.d/meshtastic.list
wget https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo/meshtastic-apk.pem -O /etc/apk/keys/meshtastic-apk.pem
apk update
```

Please note that there may be delay in [jsDelivr CDN](https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo) cache updates compared to [the repo at GitHub](https://openwrt.meshtastic.org) which may cause `apk` to pull older files and/or complain about wrong signature.

---

### OPKG
Used in old-stable versions of OpenWRT.

Supported versions:
- `24.10`
- `23.05`
- `22.03`

##### Add OPKG repository to your OpenWRT device (GitHub)

```sh
opkg update
opkg install wget-ssl
wget -O /tmp/meshtastic-ipk.pub https://openwrt.meshtastic.org/meshtastic-ipk.pub
opkg-key add /tmp/meshtastic-ipk.pub && rm /tmp/meshtastic-ipk.pub
sed -i '/meshtastic/d' /etc/opkg/customfeeds.conf
ARCH=$( . /etc/openwrt_release; echo "$DISTRIB_ARCH" )
WRT_VER=$( . /etc/openwrt_release; echo "${DISTRIB_RELEASE%%-*}" | cut -d. -f1-2 )
echo "src/gz meshtastic https://openwrt.meshtastic.org/openwrt-${WRT_VER}/${ARCH}" >> /etc/opkg/customfeeds.conf
opkg update
```

##### Add OPKG repository to your OpenWRT device (jsDelivr)
Only use in regions where GitHub is blocked 🇨🇳

```sh
opkg update
opkg install wget-ssl
wget -O /tmp/meshtastic-ipk.pub https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo/meshtastic-ipk.pub
opkg-key add /tmp/meshtastic-ipk.pub && rm /tmp/meshtastic-ipk.pub
sed -i '/meshtastic/d' /etc/opkg/customfeeds.conf
ARCH=$( . /etc/openwrt_release; echo "$DISTRIB_ARCH" )
WRT_VER=$( . /etc/openwrt_release; echo "${DISTRIB_RELEASE%%-*}" | cut -d. -f1-2 )
echo "src/gz meshtastic https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo/openwrt-${WRT_VER}/${ARCH}" >> /etc/opkg/customfeeds.conf
opkg update
```

Please note that there may be delay in [jsDelivr CDN](https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo) cache updates compared to [the repo at GitHub](https://openwrt.meshtastic.org) which may cause `opkg` to pull older files and/or complain about wrong signature.

---

### Snapshot (master) builds

For testing only. Please do not file issues about SNAPSHOT builds.

##### Add APK repository to your OpenWRT device (GitHub)

```sh
echo "https://openwrt.meshtastic.org/main/$(cat /etc/apk/arch)/packages.adb" > /etc/apk/repositories.d/meshtastic.list
wget https://openwrt.meshtastic.org/meshtastic-apk.pem -O /etc/apk/keys/meshtastic-apk.pem
apk update
```
