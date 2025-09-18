# Complete Corresponding Source (CCS) for my OpenWrt-based firmware

**WAN Load Balancer**

This repository provides the **Complete Corresponding Source (CCS)** for the OpenWrt-based images I distribute for the following devices:

- **rb750gr3**
- **rb5009**
- **hap-ac2**

⚠️ Based on OpenWrt (GPLv2). Not affiliated with or endorsed by the OpenWrt project.”

The goal is to comply with free/open-source licenses (especially **GPLv2**) and to enable anyone to **reproduce the same images** from source.

## What is included (per target)
Inside each target folder you will find:

- `configs/diffconfig` — the build configuration that matches the shipped image.
- `feeds.conf` — feed definitions used to fetch packages at build time.
- `files-public/` — public overlay files (e.g., default `/etc/config/*`) required to run the GPL components.
- `patches/` — any local patches I applied to OpenWrt or packages (if any).
- `scripts/build.sh` — a simple, reproducible build script.

There may also be `OPENWRT_COMMIT` and `OPENWRT_REMOTE` indicating the exact OpenWrt tree this build was based on (when applicable).

## What is NOT included (private MicroPython UI)
My **MicroPython-based web UI** and related private code are **not** included here.  
They are separate programs (mere aggregation) and are not derived from GPL code. Therefore, they are not part of the GPLv2 CCS requirement. The distributed commercial image contains that private UI; the publicly published CCS here contains everything required to rebuild the **OpenWrt base** and GPL-covered parts.

> If you rebuild using this CCS, you will get a functional OpenWrt-based image with the open-source components. You can add your own applications locally before building if desired.

## How to rebuild (quick start)
1. Install OpenWrt build prerequisites on your Linux host (gcc, g++, make, zlib, etc.).
2. Build host: Ubuntu 22.04.4 LTS jammy x86_64
3. Clone or unpack an OpenWrt buildroot matching the intended device and enter it, e.g.:
   ```bash
   git clone https://github.com/openwrt/openwrt.git openwrt
   cd openwrt
   git pull
   git tag
   git checkout v24.10.1
   git describe --tags
   v24.10.1
   ./scripts/feeds update -a
   ./scripts/feeds install -a
   make menuconfig
   Target System	 >  Marvell EBU Armada
   Sub-target	 >  Marvell Armada 7k/8k (ARM64)
   Target Profile > MikroTik RB5009
   ./scripts/feeds update -a
   ./scripts/feeds install mwan3 irqbalance micropython-mbedtls micropython-lib
   ./scripts/feeds update -a
   ./scripts/feeds install -a


