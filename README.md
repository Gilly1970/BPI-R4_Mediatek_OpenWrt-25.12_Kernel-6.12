# $$\color{blue}\large{\textbf{BPI-R4\ Mediatek\ (OpenWrt\ 25.12/Kernel\ 6.12)}}$$

Script to Build (Openwrt 25.12/kernel 6.12) with the mtk-openwrt-feeds...

## **To build with the Mediatek (OpenWrt 25.12/Kernel 6.12)**

1. If you want to build with the latest openwrt-25.12/kernels 6.12 and the latest mtk commits leave both OPENWRT_COMMIT="" & MTK_FEEDS_COMMIT="" empty.

2. If you want to target a specific commit use the full commit hash e.g... OPENWRT_COMMIT="2acfd9f8ab12e4f353a0aa644d9adf89588b1f0f"

3. Error Checks - All scripts and patches will be auto chacked with dos2unix and corrected if needed if they are not in the correct EOL format.

## Compile Environment Requirement

- Minimum requirement: Ubuntu 22.04

##### Toolchain

- Installs essential development tools and libraries, including compilers, build tools. Please refer to https://openwrt.org/docs/guide-developer/toolchain/install-buildsystem for more detail
     ```csharp
     sudo apt update
     sudo apt install build-essential clang flex bison g++ gawk \
     gcc-multilib g++-multilib gettext git libncurses-dev libssl-dev \
     python3-distutils python3-setuptools rsync swig unzip zlib1g-dev file wget \
     u-boot-tools dos2unix
     ```
## **How to Use**

1. **Clone repo**:
   * Clone repo: 
     ```csharp
     git clone https://github.com/Gilly1970/BPI-R4_Mediatek_OpenWrt-25.12_Kernel-6.12.git
     ```
   * Update permissions: 
     ```csharp
     sudo chmod 775 -R BPI-R4_Mediatek_OpenWrt-25.12_Kernel-6.12
     ```

2. **Run the Script**:  
   * Make the script executable:
     ```csharp
     chmod +x mtk-openwrt_25.12_build.sh
	 ```
     
   * Execute the script: 
     ```csharp
     ./mtk-openwrt_25.12_build.sh
	 ```

## **Filogic 880/850 WiFi7 4.3 Alpha Release (2025-12-31)**
> [!WARNING]
> This build is for testing the Alpha Release which may contain bugs so if you want stability please use Openwrt 24.10 instead.
>
## **Troubleshooting Build Errors**

If you encounter errors during compilation, they are often caused by recent patches released by MediaTek (this is less common with OpenWrt patches).

To resolve this, you have two options:

**1. Pin a specific commit:** Identify the last working commit before the update that broke the build. Change the MTK_FEEDS_COMMIT variable to that specific hash.

- **Change:** `readonly MTK_FEEDS_COMMIT=""`

- **To:** `readonly MTK_FEEDS_COMMIT="5dcc2867b180400f93664d6ed343d32b1ce06428"`

**2. Wait for a fix:** Wait for MediaTek to release a subsequent patch that resolves the issue.

To check MediaTek patches releases - https://git01.mediatek.com/plugins/gitiles/openwrt/feeds/mtk-openwrt-feeds/+log

To check OpenWrt patches releases - https://git.openwrt.org/?p=openwrt/openwrt.git;a=shortlog;h=refs/heads/openwrt-25.12

# $$\color{blue}\large{\textbf{Notes}}$$

- 11.02.2026 - Added new eeprom containing zeros patch ```0140-wifi-mt76-mt7996-use-mt76_get_txpower_cur.patch```.

  - I've had to rebuild the patch from the ground up to make it work again with the current MTK-feeds. However, it does need a lot more work due to all the recent wifi-mt76 driver changes in kernel-6.12. In particular the removal of the `mt7996_get_txpower` function which all the old eeprom containing zero patches relied on to work.
  
  - This patch is a work in progress and in its current state will allow you to change the default tx power levels on all radios as long as you have `option sku_idx '0'` in your wireless config. When the image is first installed you might see the default levels still showing very low on the 2 Ghz & 6 Ghz bands.. Once you manually toggle to the desired tx power level e.g. `23 dBm` and save, your should see the correctly defaults show for your region.

- 02.02.2026 - Temp patched the `openwrt_helpers.sh` file to replce 'https:' with 'git:' during the update feeds process.. Changing to git: helps with all the curent errors coming from https://git.openwrt.org the last week or so.
  - If you don't need it just remove `autobuild/unified/scripts/openwrt_helpers.sh` from the `mtk-add-patch` file.

