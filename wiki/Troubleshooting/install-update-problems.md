---
title: "💾 Install & Update Problems"
description: "Known issues that cause install and update problems in Star Citizen on Linux + troubleshooting steps to resolve them"
parent: "Troubleshooting"
nav_order: 1
md_message: "You are viewing raw source files... Go to https://wiki.starcitizen-lug.org/ to use the wiki!"
---

# 💾 Install & Update Problems

## Wine prefix creation failed
- If the LUG Helper install log shows an error similar to:  
  `warning: WINE is /path/to/bin/wine, which is neither on the path nor an executable file`  
  To fix, `cat /proc/mounts` and make sure the mount point is not marked `noexec`. You may need to explicitly set `defaults` or `exec`.
- If the install log shows an error similar to:  
  `SHA256 mismatch` or `no valid cabinets found`  
  To fix, delete the winetricks cache in `~/.cache/winetricks/` and try installing again


## RSI Launcher installation hangs at Updating Game Content
- The Launcher sometimes hangs during this phase of the install process
- Completely quit the launcher, ensuring no lingering wine processes remain, then verify files


## RSI Launcher error: Unable to Create Folder
- This is a [known issue](https://robertsspaceindustries.com/spectrum/community/SC/forum/1/thread/rsi-launcher-2-10-0-release-notes) with the RSI Launcher, possible error code 8004
- Manually create the LIVE/PTU/TECH-PREVIEW directory after installing the RSI Launcher with the Helper. For a default install path, you can run:
  ```
  mkdir -p "~/Games/star-citizen/drive_c/Program Files/Roberts Space Industries/StarCitizen/LIVE"
  ```


## RSI Launcher fails to start
- Possible cause: Outdated glibc
  - Log message may include `could not load ntdll.so ... version 'GLIB-C_x.xx not found'`
  - Update to the latest release of a [non-LTS distro](/Tips-and-Tricks#recommended-distros)


## RSI Launcher executable is missing
- Automatic update sometimes fails or is interrupted
- Follow manual update [instructions](/Tips-and-Tricks#rsi-launcher-manual-update)


## RSI Launcher doesn't auto-update
- Follow manual update [instructions](/Tips-and-Tricks#rsi-launcher-manual-update)


## RSI Launcher freezes within a few seconds of opening
- Try using a different [wine runner](/Tips-and-Tricks#recommended-runners)


## RSI Launcher Black or white window
- Try editing the [launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) to add the RSI Launcher flags `--in-process-gpu --disable-gpu`. For example:
  ```
    "$wine_path"/wine "C:\Program Files\Roberts Space Industries\RSI Launcher\RSI Launcher.exe" --in-process-gpu --disable-gpu > "$launch_log" 2>&1
  ```


## RSI Launcher empty or crash
- Try logging out and back in, or reset the launcher by pressing Ctrl+Shift+Alt+R
- Delete the rsilauncher directory in the wine prefix's Appdata  
  `star-citizen/drive_c/users/<your username here>/AppData/Roaming/rsilauncher`
- Try disabling Nvidia [Smooth Motion](/Troubleshooting/nvidia#nvidia-smooth-motion)
- If using Pop!_OS Cosmic, this is a [known issue](https://github.com/pop-os/cosmic-epoch/issues/2368).
  - Try using the [LUG Helper](/Tips-and-Tricks#how-to-run-the-lug-helper)'s `Open Wine prefix configuration`  
    option in the Maintenance menu to turn on virtual desktop mode
  - Try xwayland-run package
    ```
    ############################################################################
    # Launch the game
    ############################################################################
    xwayland-run -- "$wine_path"/wine "C:\Program Files\Roberts Space Industries\RSI Launcher\RSI Launcher.exe" > "$launch_log" 2>&1
    ```
  - Try switching to [Experimental Wine Wayland](/Tips-and-Tricks#wine-wayland)
  - Try [gamescope](/Tips-and-Tricks#gamescope), or an alternative compositor


## RSI Launcher minimizes and won't re-open
- Try to restore the window using the taskbar icon
- If that doesn't work, [open your Wine prefix](/Tips-and-Tricks#where-is-my-wine-prefix-where-is-my-liveptu-directory), then delete the rsilauncher directory in the wine prefix's Appdata  
  `star-citizen/drive_c/users/<your username here>/AppData/Roaming/rsilauncher`
- To avoid the problem in the future, turn on `Enable close-to-quit` in the RSI Launcher settings


## RSI Launcher indicates You are currently offline
- Log out and back in


## Launch Error - Settings.json not found
- Verify game files


## RSI Launcher Error Code 60101
- [Issue Council STARC-198177](https://issue-council.robertsspaceindustries.com/projects/STAR-CITIZEN/issues/STARC-198177)
- Use a [LUG Wine Runner](/Tips-and-Tricks#recommended-runners) 10.13-2 or newer to prevent the popup
- This error does not prevent the game from running, the game will launch shortly!


## RSI Launcher Error Code 3221225477
- Use winetricks to install `vcrun2022` in your wine prefix
- Open a [Wine maintenance shell](/Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) then run `winetricks -q vcrun2022` then `exit`


## RSI Launcher Error Code 3004/3005/5006/5008
- RSI Launcher may crash at calculating disk space.
- Log may show *"[Pipeline] Phase compute_size timed out after 60000ms, cancelling and skipping."*
- Sometimes caused by a slow or unreliable network connection.

1. [Locate your Star Citizen LIVE](/Tips-and-Tricks#where-is-my-wine-prefix-where-is-my-liveptu-directory) directory.
2. Create a new empty file in your LIVE directory named `Data.p4k.part`
3. If you're installing the game for the first time, also create a new empty file named `Data.p4k`
4. Re-launch the game and try the update or verify again.


## Installing Star Citizen on an NTFS-formatted drive
- Don't; it probably won't work and will likely only corrupt your game files.


## Popup warning 64-bit Windows is required
- Ensure that you are using a [Recommended](/Tips-and-Tricks#recommended-distros) 64 bit linux distro
- Override environment variable WINEARCH=64


## openSUSE Tumbleweed: Wine prefix creation failed
- If SELinux is enabled (default) on openSUSE, the `selinux-policy-targeted-gaming` package is [required](https://en.opensuse.org/Portal:SELinux/Common_issues#Steam_Proton,_Bottles,_WINE,_Lutris,_not_working) or game installation will fail.
- Manually install `selinux-policy-targeted-gaming` from the openSUSE repos. Alternatively, both Steam and Lutris pull in this package as a dependency.
