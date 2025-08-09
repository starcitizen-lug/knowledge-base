---
title: "💾 Install & Update Problems"
nav_order: 3
---

#### General troubleshooting steps
- Refer to [First things to try](#first-things-to-try) above.
- Make sure you are not trying to install to an NTFS-formatted drive.
- Be sure you haven't changed the default install path in the RSI Launcher settings. If you wish to install the game elsewhere, put the entire wine prefix there instead.


#### Wine prefix creation failed
- LUG Helper install log shows error similar to `warning: WINE is /path/to/.../bin/wine, which is neither on the path nor an executable file`
- To fix, make sure the mount point is not marked `noexec`


#### Launcher installation hangs at Updating Game Content
- The Launcher sometimes hangs during this phase of the install process
- Completely quit the launcher, ensuring no lingering wine processes remain, then verify files


#### Wine install fails to create .desktop files
- Manually create a file `~/.local/share/applications/RSI Launcher.desktop` based on the following template.
- Edit paths based on your install, then update the cache by running `update-desktop-database ~/.local/share/applications`
  ```
  [Desktop Entry]
  Name=RSI Launcher
  Exec="/home/{user}/Games/StarCitizen/sc-launch.sh"
  Type=Application
  StartupNotify=true
  Comment=RSI Launcher
  Path=/home/{user}/Games/StarCitizen/dosdevices/c:/Program\sFiles/Roberts\sSpace\sIndustries/RSI\sLauncher
  Icon=rsi-launcher.png
  StartupWMClass=rsi launcher.exe
  ```

#### RSI Launcher Error Code 2000
- Follow [Launcher Tips](Tips-and-Tricks#rsi-launcher-20) instructions


#### RSI Launcher executable is missing
- Automatic update sometimes fails or is interrupted
- Follow manual update [instructions](Tips-and-Tricks#rsi-launcher-manual-update)

#### RSI Launcher doesn't auto-update
- Follow manual update [instructions](Tips-and-Tricks#rsi-launcher-manual-update)

#### RSI Launcher error: *Could not fix permissions on directory*
- Please follow our [step-by-step guide](Tips-and-Tricks#rsi-launcher-20) for the 2.0 RSI Launcher

#### Installing Star Citizen on an NTFS-formatted drive
- Don't; it probably won't work and will likely only corrupt your game files.

#### Popup warning 64-bit Windows is required
- Ensure that you are using a [Recommended](Tips-and-Tricks#recommended-distros) 64 bit linux distro
- Override environment variable WINEARCH=64