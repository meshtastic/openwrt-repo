# Meshtastic OpenWrt Repo

Home to our APK and OPKG repositories for easily installing Meshtastic on OpenWrt-supported routers.

If you're looking for the package source code, check out [meshtastic/openwrt](https://github.com/meshtastic/openwrt).

## Supported OpenWrt versions
- `SNAPSHOT` (`main` branch)
- `24.10` (stable)
- `23.05` (old-stable)
- `22.03` (old-stable)

## How to use

This repository is currently hosted on [GitHub Pages](https://github.com). If you have problems accessing [this repo](https://openwrt.meshtastic.org) or access to GitHub [may be blocked](https://en.wikipedia.org/wiki/Censorship_of_GitHub) in your country, skip to the `Add repository to your OpenWrt device (jsDelivr)` sections. Both repositories use HTTPS protocol and require one of the SSL support packages to be installed on your router.

### OPKG
Used in stable versions of OpenWrt.

Supported versions:
- `24.10`
- `23.05`
- `22.03`

##### Add OPKG repository to your OpenWrt device (GitHub)

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

##### Add OPKG repository to your OpenWrt device (jsDelivr)
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

### APK
Used in `SNAPSHOT` (`main`) builds. For stable OpenWrt versions see `OPKG` above.

##### Add APK repository to your OpenWrt device (GitHub)

```sh
echo "https://openwrt.meshtastic.org/main/$(cat /etc/apk/arch)/packages.adb" > /etc/apk/repositories.d/meshtastic.list
wget https://openwrt.meshtastic.org/meshtastic-apk.pem -O /etc/apk/keys/meshtastic-apk.pem
apk update
```

##### Add APK repository to your OpenWrt device (jsDelivr)
Only use in regions where GitHub is blocked 🇨🇳

```sh
echo "https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo/main/$(cat /etc/apk/arch)/packages.adb" > /etc/apk/repositories.d/meshtastic.list
wget https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo/meshtastic-apk.pem -O /etc/apk/keys/meshtastic-apk.pem
apk update
```

Please note that there may be delay in [jsDelivr CDN](https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo) cache updates compared to [the repo at GitHub](https://openwrt.meshtastic.org) which may cause `apk` to pull older files and/or complain about wrong signature.
