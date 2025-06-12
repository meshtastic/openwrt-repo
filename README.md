# Meshtastic OpenWRT Repo

Home to our APK and OPKG repositories for easily installing Meshtastic on OpenWRT-supported routers.

If you're looking for the package source code, check out [meshtastic/openwrt](https://github.com/meshtastic/openwrt).

## Supported OpenWRT versions
- `SNAPSHOT` (master branch)

`24.10` and `23.05` support coming soon.

## How to use

This repository is currently hosted on [GitHub Pages](https://github.com). If you have problems accessing [this repo](https://openwrt.meshtastic.org) or access to GitHub [may be blocked](https://en.wikipedia.org/wiki/Censorship_of_GitHub) in your country, skip to the `Add repository to your OpenWrt device (jsDelivr)` sections. Both repositories use HTTPS protocol and require one of the SSL support packages to be installed on your router.

### APK
Used in `SNAPSHOT` (master) builds. For stable OpenWRT versions see `OPKG` below.

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


### OPKG
Used in stable versions of OpenWRT.

Supported versions:
- `24.10`

##### Add OPKG/IPK repository to your OpenWRT device (GitHub)

```sh
# Coming soon
```

##### Add OPKG/IPK repository to your OpenWRT device (jsDelivr)
Only use in regions where GitHub is blocked 🇨🇳

```sh
# Coming soon
```

Please note that there may be delay in [jsDelivr CDN](https://cdn.jsdelivr.net/gh/meshtastic/openwrt-repo) cache updates compared to [the repo at GitHub](https://openwrt.meshtastic.org) which may cause `opkg` to pull older files and/or complain about wrong signature.
