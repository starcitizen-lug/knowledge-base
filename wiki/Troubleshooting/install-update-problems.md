---
title: "💾 Install & Update Problems"
description: "Known issues that cause install and update problems in Star Citizen on Linux + troubleshooting steps to resolve them"
parent: "Troubleshooting"
nav_order: 1
---

# 💾 Install & Update Problems

## Wine prefix creation failed
- LUG Helper install log shows error similar to `warning: WINE is /path/to/.../bin/wine, which is neither on the path nor an executable file`
- To fix, make sure the mount point is not marked `noexec`


## Launcher installation hangs at Updating Game Content
- The Launcher sometimes hangs during this phase of the install process
- Completely quit the launcher, ensuring no lingering wine processes remain, then verify files


## Wine install fails to create .desktop files
- Manually create a file `~/.local/share/applications/RSI Launcher.desktop` based on the following template. Be sure to update the `Exec=` and `Path=` lines!
- Edit paths based on your install, then update the cache by running `update-desktop-database ~/.local/share/applications`
  ```
  [Desktop Entry]
  Name=RSI Launcher
  Type=Application
  Comment=RSI Launcher
  Keywords=Star Citizen;StarCitizen
  StartupNotify=true
  StartupWMClass=rsi launcher.exe
  Icon=rsi-launcher.png
  Exec="/home/{user}/Games/StarCitizen/sc-launch.sh"
  Path=/home/{user}/Games/StarCitizen/dosdevices/c:/Program\sFiles/Roberts\sSpace\sIndustries/RSI\sLauncher
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
