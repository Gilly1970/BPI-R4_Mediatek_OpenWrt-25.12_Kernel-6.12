# $$\color{blue}\large{\textbf{BPI-R4\ Mediatek\ (OpenWrt\ 25.12/Kernel\ 6.12)}}$$

Script to Build (Openwrt 25.12/kernel 6.12) with the mtk-openwrt-feeds...

## **To build with the Mediatek (OpenWrt 25.12/Kernel 6.12)**

1. If you want to build with the latest openwrt-25.12/kernels 6.12 and the latest mtk commits leave both OPENWRT_COMMIT="" & MTK_FEEDS_COMMIT="" empty.

2. If you want to target a specific commit use the full commit hash e.g... OPENWRT_COMMIT="2acfd9f8ab12e4f353a0aa644d9adf89588b1f0f"

3. Error Checks - All scripts and patches will be auto checked with dos2unix and corrected if needed if they are not in the correct EOL format.

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

 - 24.02.2026 - Removed the commits in the script again so it is now pulling from the latest again.
 
	 - MTK have updated with another [fix patches](https://git01.mediatek.com/plugins/gitiles/openwrt/feeds/mtk-openwrt-feeds/+/ff9029576c3c07cdeed9dda8de7f8e9d8f996dcd) which caused the latest round of build conflicts.
	   If the build breaks agian due to patch conflicts just set the mtk & openwrt to the last commits before
	   the build fail and wait for MTK to release another fix before opening it up again. I will no longer
	   be making any more changes to this repo as I have moved away from the BPI-R4 platform completly.

 - 20.02.2026 - Added 0145-mtk-new_tx_power_check.patch
 
    - This is the final patch for the BE14 card that I will be adding to the repo. After a long battle with driver 
	  issues and zeroed EEPROMs in the hopes of a Sinovoip-led solution, I’m calling it.
	  
	  The hardware is fundamentally flawed—burdened by excessive noise and poor signal quality. The chances of a 
	  fix via new firmware at this stage are slim to none, and Slim just left town. I am officially dropping my BE14
	  card into the recycling bin and will be focused on more reputable hardware that I've purchased as a replacement.

