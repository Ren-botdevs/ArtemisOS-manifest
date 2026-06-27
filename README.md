# ArtemisOS

<p align="center">
  <img src="https://raw.githubusercontent.com/Ren-botdevs/ArtemisOS-manifest/refs/heads/main/1782575429295.png" width="200" alt="ArtemisOS Logo Placeholder" />
</p>

<p align="center">
  <b>ArtemisOS</b> — A privacy-focused, de-Googled Android distribution based on LineageOS.
</p>

<p align="center">
  <a href="#overview">Overview</a> •
  <a href="#features">Features</a> •
  <a href="#syncing-the-source">Sync</a> •
  <a href="#building">Build</a> •
  <a href="#credits">Credits</a> •
  <a href="#license">License</a>
</p>

---

## Overview

ArtemisOS is a custom Android ROM built on top of **LineageOS**, stripped of Google proprietary services and telemetry to deliver a clean, privacy-first mobile experience. We believe your device should serve you — not advertisers or data brokers.

By removing Google Mobile Services (GMS) and replacing them with open-source alternatives, ArtemisOS gives you full control over your data while maintaining the stability and maturity of the LineageOS base.

## Features

| Feature | Description |
|---------|-------------|
| 🔒 **De-Googled** | Google Mobile Services (GMS), Play Services, and related telemetry completely removed |
| 🛡️ **Privacy-First** | Hardened defaults, minimal data collection, no background connections to Google servers |
| 📦 **MicroG Ready** | Optional signature spoofing support for users who choose to install MicroG |
| 🎨 **LineageOS Base** | Inherits LineageOS stability, device support, and feature set |
| ⚡ **Performance** | Optimized build flags and debloated system image for snappier performance |
| 🧩 **Open Source** | Fully open source — build it, audit it, trust it |

## Syncing the Source

### Prerequisites

- A machine running **Linux** (Ubuntu 22.04+ recommended)
- At least **200 GB** of free disk space
- At least **16 GB** of RAM (32 GB recommended)
- A stable internet connection

### 1. Install Required Packages

```bash
sudo apt update && sudo apt install -y     git-core gnupg flex bison build-essential zip curl     zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386     libncurses5-dev lib32ncurses5-dev x11proto-core-dev     libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils     xsltproc unzip fontconfig python3 python3-pip     repo ccache
```

### 2. Configure Git

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

### 3. Initialize Repo & Sync

Create a working directory and initialize the ArtemisOS manifest:

```bash
mkdir -p ~/artemis && cd ~/artemis

# Initialize the repo with ArtemisOS manifest
repo init -u https://github.com/ArtemisOS/android_manifest.git -b main --git-lfs

# Sync the source (this may take a while)
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
```

> 💡 **Tip:** Use `ccache` to speed up subsequent builds:
> ```bash
> export USE_CCACHE=1
> export CCACHE_EXEC=/usr/bin/ccache
> ccache -M 50G
> ```

## Building

### 1. Set Up Environment

```bash
cd ~/artemis
source build/envsetup.sh
```

### 2. Lunch Your Device

Replace `<device_codename>` with your device's codename (e.g., `raphael`, `davinci`, `instantnoodle`):

```bash
lunch lineage_<device_codename>-userdebug
```

### 3. Start the Build

```bash
mka bacon -j$(nproc --all)
```

The build process will take anywhere from **1 to 4 hours** depending on your hardware. Once complete, the flashable ZIP will be located at:

```
out/target/product/<device_codename>/ArtemisOS-*.zip
```

### Build Variants

| Command | Description |
|---------|-------------|
| `lunch lineage_<device>-userdebug` | Debug build with root access |
| `lunch lineage_<device>-user` | Production build (recommended for daily use) |
| `lunch lineage_<device>-eng` | Engineering build with extra debugging tools |

## Flashing

1. Boot into **Recovery** (TWRP / Lineage Recovery / etc.)
2. Wipe **System**, **Data**, **Cache**, and **Dalvik/ART Cache**
3. Flash the ArtemisOS ZIP
4. (Optional) Flash [MicroG](https://microg.org/) or your preferred app store (F-Droid, Aurora Store)
5. Reboot and enjoy your privacy-first Android experience

## Device Support

ArtemisOS inherits device support from LineageOS. If your device is officially supported by LineageOS, it is likely compatible with ArtemisOS as well. Community maintainers are welcome to submit device trees.

To add support for a new device, fork the relevant device, kernel, and vendor repositories, then submit a merge request to our manifest.

## Contributing

We welcome contributions! Whether it's bug fixes, new features, or device support, feel free to open an issue or submit a pull request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Credits

ArtemisOS would not be possible without the incredible work of the following projects and communities:

- **[AOSP (Android Open Source Project)](https://source.android.com/)** — The foundation of Android. Without Google's open-source base, custom ROMs would not exist.
- **[LineageOS](https://lineageos.org/)** — The base upon which ArtemisOS is built. Huge thanks to the LineageOS team for their years of dedication to the custom ROM ecosystem.
- **[AOSPA (Paranoid Android)](https://paranoidandroid.co/)** — For pioneering features and design philosophies that continue to inspire the custom ROM community.
- **[GrapheneOS](https://grapheneos.org/) & [CalyxOS](https://calyxos.org/)** — For pushing the boundaries of privacy and security on Android.
- **All open-source contributors, device maintainers, and testers** — Your work keeps the community alive.

## License

ArtemisOS is licensed under the **Apache License 2.0**, in line with AOSP and LineageOS licensing. See [LICENSE](LICENSE) for details.

> ⚠️ **Disclaimer:** ArtemisOS is not affiliated with Google, LineageOS, or AOSPA. All trademarks belong to their respective owners. Flash at your own risk — we are not responsible for bricked devices, dead SD cards, or thermonuclear war.

---

<p align="center">
  Made with ❤️ by the ArtemisOS Team
</p>
