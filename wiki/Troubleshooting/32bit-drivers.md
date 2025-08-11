---
title: "👾 32bit Drivers"
parent: "Troubleshooting"
nav_order: 6
---

# 👾 32bit Drivers

## Arch-based Distributions (Arch, EndeavourOS, Manjarno, etc)
1. Enable the [multilib repo](https://wiki.archlinux.org/title/Official_repositories#Enabling_multilib)
2. Install 32bit drivers
- AMD
  ```
  sudo pacman -S --needed lib32-mesa vulkan-radeon lib32-vulkan-radeon vulkan-icd-loader lib32-vulkan-icd-loader
  ```
- Nvidia
  ```
  sudo pacman -S --needed nvidia-dkms nvidia-utils lib32-nvidia-utils nvidia-settings vulkan-icd-loader lib32-vulkan-icd-loader
  ```

## Ubuntu & Friends (Ubuntu, Mint, PopOS, etc)
- AMD
  ```
  sudo dpkg --add-architecture i386 && sudo apt update && sudo apt upgrade && sudo apt install libgl1-mesa-dri:i386 mesa-vulkan-drivers mesa-vulkan-drivers:i386
  ```
- Nvidia
  ```
  sudo dpkg --add-architecture i386 && sudo apt update && sudo apt install -y nvidia-driver-525 libvulkan1 libvulkan1:i386
  ```

## Fedora & Derivatives (Fedora, Nobara, etc)
- TBA

## openSUSE Tumbleweed
- AMD
  ```
  sudo zypper in kernel-firmware-amdgpu libdrm_amdgpu1 libdrm_amdgpu1-32bit libdrm_radeon1 libdrm_radeon1-32bit libvulkan_radeon libvulkan_radeon-32bit libvulkan1 libvulkan1-32bit
  ```
- Nvidia
   1. Follow the instructions here: https://en.opensuse.org/SDB:NVIDIA_drivers
   2. Install 32bit drivers by appending the `-32bit` suffix to the driver package names
   3. Install vulkan libraries:
      ```
      sudo zypper in libvulkan1 libvulkan1-32bit
      ```

## Gentoo 💪
- We defer to your expertise
