# Kernel Build Script for the Samsung Galaxy A56 - SM-A566B

[![Build with SukiSU SuSFS](https://github.com/dx4m/kernel-buildscript-a566b/actions/workflows/build_suki.yml/badge.svg)](https://github.com/dx4m/kernel-buildscript-a566b/actions/workflows/build_suki.yml)
[![Build with KernelSU SuSFS](https://github.com/dx4m/kernel-buildscript-a566b/actions/workflows/build_ksu.yml/badge.svg)](https://github.com/dx4m/kernel-buildscript-a566b/actions/workflows/build_ksu.yml)
[![Build clean Kernel](https://github.com/dx4m/kernel-buildscript-a566b/actions/workflows/build_clean.yml/badge.svg)](https://github.com/dx4m/kernel-buildscript-a566b/actions/workflows/build_clean.yml)
[![Issues](https://img.shields.io/github/issues/dx4m/kernel-buildscript-a566b?color=%230055AA)](https://github.com/dx4m/kernel-buildscript-a566b/issues)
[![Pull Requests](https://img.shields.io/github/issues-pr/dx4m/kernel-buildscript-a566b?color=%230055AA)](https://github.com/dx4m/kernel-buildscript-a566b/pulls)
![GitHub Downloads (specific asset, all releases)](https://img.shields.io/github/downloads/dx4m/kernel-buildscript-a566b/boot.img.tar?color=%2300AA11)
![GitHub Downloads (specific asset, all releases)](https://img.shields.io/github/downloads/dx4m/kernel-buildscript-a566b/boot.img?color=%2300AA11)

This repository contains a simple build script and environment setup for compiling the **Samsung Galaxy A56 (SM-A566B)** kernel based on the AOSP toolchain and Samsung kernel sources.
It was made so the A56 community has an updated kernel because of Luciiuss left.

## Intro

- Automated setup of the Android build toolchain (prebuilts, clang, kernel build tools, etc.)
- Support for custom build arguments (e.g. `--enable-ksu`, `--enable-suki`, `--disable-suki`) - Use `--help` for more info
- `--disable-samsung-protection` is enabled by default, otherwise your device won't boot.
- Actions support

## Requirements

- Linux environment (tested on WSL2 + Ubuntu)
- Install dependencies:
  ```bash
  sudo apt-get update
  sudo apt-get install git make bc bison flex libssl-dev wget curl lzop git-core gnupg flex bison build-essential zip zlib1g-dev libc6-dev-i386 x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig python3 repo -y
  ```
  or use
  ```bash
  ./install_dep.sh
  ```
- Sufficient disk space (~100GB+ recommended)

## Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/dx4m/kernel-buildscript-a566b.git
   cd kernel-buildscript-a566b
   chmod +x *.sh
   ```

2. Install dependencies:
   ```bash
   ./install_dep.sh
   ```
   
   and then you need to setup your identity
   ```bash
   git config --global user.email "your@email.com"
   git config --global user.name "Your Name"
   ```

3. Setup the toolchain with SukiSU Ultra and SuSFS (downloads AOSP prebuilts):
   
   ```bash
   ./setup_buildchain.sh
   ```
   
  - To setup the toolchain with KernelSU instead of SukiSU Ultra use:
	```bash
	./setup_buildchain.sh --enableKSU --enableSuSFS
	```
	or without SuSFS:
	```bash
	./setup_buildchain.sh --enableKSU --disableSuSFS
	```
	
  - To setup with clean sources:
	```bash
	./setup_buildchain.sh --disableSuki --disableSuSFS
	```

4. Build the kernel:
   ```bash
   ./build_kernel.sh
   ```

  - To build with KernelSU instead of SukiSU Ultra:
	```bash
	./build_kernel.sh --enable-ksu
	```

  - Build clean kernel:
	```bash
	./build_kernel.sh --disable-suki --disable-samsung-protection
	```

  - For help use:
	```bash
	./build_kernel.sh --help
	```

5. The compiled kernel output will be placed in:
   ```
   out/arch/arm64/boot/
   ```
   and a flashable boot.img & boot.img.tar will be generated in the root of the repo.

## License

This project is licensed under the **GNU General Public License v3.0** (GPL-3.0).  
See the [LICENSE](LICENSE) file for details.

## Credits
Special thanks to:
- [Samsung](https://opensource.samsung.com/) for releasing the [kernel sources](https://opensource.samsung.com/uploadSearch?searchValue=sm-a566b)
- [Lucius](https://github.com/Luciiuss) for his buildscript and [kernel](https://github.com/Luciiuss/sm-a566b) for the Galaxy A56 (OUTDATED!).

## Resources
- [AOSP Kernel Sources](https://android.googlesource.com/kernel/manifest/)
- [Samsung Kernel Source](https://github.com/dx4m/android-kernel-samsung-a566b)
- [Kernel Buildscript](https://github.com/dx4m/kernel-buildscript-e1s) for the S24 where this bases on
- [SukiSU Ultra Project](https://github.com/sukisu-ultra/sukisu-ultra)
- [KernelSU Project](https://github.com/tiann/KernelSU)
- [susfs4ksu](https://gitlab.com/simonpunk/susfs4ksu)
- [HymoFS](https://github.com/Anatdx/HymoFS)
