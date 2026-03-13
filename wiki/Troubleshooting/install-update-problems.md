---
title: "💾 Install & Update Problems"
description: "Known issues that cause install and update problems in Star Citizen on Linux + troubleshooting steps to resolve them"
parent: "Troubleshooting"
nav_order: 1
md_message: "You are viewing raw source files... Go to https://wiki.starcitizen-lug.org/ to use the wiki!"
---

# 💾 Install & Update Problems

## Wine prefix creation failed
- LUG Helper install log shows error similar to:  
  `warning: WINE is /path/to/bin/wine, which is neither on the path nor an executable file`  
  To fix, make sure the mount point is not marked `noexec`
- install log shows error similar to:  
  `SHA256 mismatch` or `no valid cabinets found`  
  To fix, delete the winetricks cache in `~/.cache/winetricks/` and try installing again


## Launcher installation hangs at Updating Game Content
- The Launcher sometimes hangs during this phase of the install process
- Completely quit the launcher, ensuring no lingering wine processes remain, then verify files


## RSI Launcher error: Unable to Create Folder
- This is a [known issue](https://robertsspaceindustries.com/spectrum/community/SC/forum/1/thread/rsi-launcher-2-10-0-release-notes) with the RSI Launcher, possible error code 8004
- Manually create the LIVE/PTU/TECH-PREVIEW directory after installing the RSI Launcher with the Helper. For a default install path, you can run:
  ```
  mkdir -p "~/Games/star-citizen/drive_c/Program Files/Roberts Space Industries/StarCitizen/LIVE"
  ```


## RSI Launcher executable is missing
- Automatic update sometimes fails or is interrupted
- Follow manual update [instructions](/Tips-and-Tricks#rsi-launcher-manual-update)

## RSI Launcher doesn't auto-update
- Follow manual update [instructions](/Tips-and-Tricks#rsi-launcher-manual-update)

## Installing Star Citizen on an NTFS-formatted drive
- Don't; it probably won't work and will likely only corrupt your game files.

## Popup warning 64-bit Windows is required
- Ensure that you are using a [Recommended](/Tips-and-Tricks#recommended-distros) 64 bit linux distro
- Override environment variable WINEARCH=64

## openSUSE Tumbleweed: Wine prefix creation failed
- If SELinux is enabled (default) on openSUSE, the `selinux-policy-targeted-gaming` package is [required](https://en.opensuse.org/Portal:SELinux/Common_issues#Steam_Proton,_Bottles,_WINE,_Lutris,_not_working) or game installation will fail.
- Manually install `selinux-policy-targeted-gaming` from the openSUSE repos. Alternatively, both Steam and Lutris pull in this package as a dependency.
