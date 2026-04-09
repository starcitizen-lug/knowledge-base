---
title: "🤪 Unexpected Behavior"
description: "Known issues that can cause unexpected behavior in Star Citizen on Linux + troubleshooting steps to resolve them"
parent: "Troubleshooting"
nav_order: 4
md_message: "You are viewing raw source files... Go to https://wiki.starcitizen-lug.org/ to use the wiki!"
---

# 🤪 Unexpected Behavior


## Launcher empty or crash
- Try logging out and back in, or reset the launcher by pressing Ctrl+Shift+Alt+R
- Delete the rsilauncher directory in the wine prefix's Appdata  
  `star-citizen/drive_c/users/<your username here>/AppData/Roaming/rsilauncher`
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


## Launcher indicates You are currently offline
- Log out and back in


## Launch Error - Settings.json not found
- Verify game files


## RSI Launcher Error Code 60101
- [Issue Council STARC-198177](https://issue-council.robertsspaceindustries.com/projects/STAR-CITIZEN/issues/STARC-198177)
- Use a [LUG Wine Runner](/Tips-and-Tricks#recommended-runners) 10.13-2 or newer to prevent the popup
- This error does not prevent the game from running, the game will launch shortly!


## Launch Error - %AppData% returned empty string
- Open a [Wine maintenance shell](/Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) then type `wineserver -k` to terminate all lingering Wine processes.
- If that doesn't resolve it, try switching to a different Wine runner.
- Check that you haven’t changed the default install path in the RSI Launcher settings.


## Visual glitches or semi-transparent lines, poor performance, possibly random crashes
- DXVK may be broken or disabled. Reinstall it using the LUG Helper DXVK and maintenance menus
- Your game shader cache may need to be cleared. Use the Delete Shaders option in the RSI Launcher > Settings > Games > {LIVE,PTU} > Delete Local Settings > Shaders folder


## Account login failed (possible code 19000)
This is a generic error code representing any issue with logging in to CIG servers
- Expected when attempting launch/login during a patch release
- Kill the launcher and restart it and try again
- Ensure that IPv6 is not disabled
- Check that custom firewall rules on your host or router are not blocking outbound traffic to non-HTTP(S) ports


## DirectX error message
- Error may read `Star Citizen requires DirectX feature level of 11.1 as a minimum which is not supported at present on this machine`  
  ![image](https://cdn.jsdelivr.net/gh/starcitizen-lug/knowledge-base@main/wiki/assets/images/Troubleshooting/unexpected-behavior/dx-feature-level.webp)
- If your system has an integrated gpu (ie, Intel), check that the `Vulkan device` is not set to the integrated gpu:
  - Identify device name using command `vulkaninfo --summary | grep deviceName`
  - Edit the [launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) and set the device name environment variable: `DXVK_FILTER_DEVICE_NAME=yourdevicenamehere`
  - Verify by setting the environment variable `DXVK_HUD=1` and observing the device name in the upper left of the screen
- Make sure your GPU drivers (Mesa/nvidia) are up to date
  - For AMD, be sure to use the open source radeon drivers (ie. vulkan-radeon), **not** the proprietary drivers (ie. amdvlk)
- If using DX11 rendering instead of Vulkan, make sure DXVK is enabled/updated:
  - Use the LUG Helper to [update dxvk](/Tips-and-Tricks#updating-dxvk-within-a-wine-prefix)
- Try switching to a non-staging wine runner from our [recommended runners](/Tips-and-Tricks#recommended-runners) list
- Try [downgrading](/Tips-and-Tricks#updating-dxvk-within-a-wine-prefix) to an older DXVK version


## Failed to initialize dependencies error
- Make sure the `SDL_VIDEODRIVER` environment variable is **NOT** set globally to `wayland` on your system: `env | grep SDL_VIDEODRIVER`
- If it is set, remove it from whichever environment config(s) is setting it.
- [Edit the launch script](#how-to-edit-the-launch-script) and add `unset SDL_VIDEODRIVER` to the environment variables section


## Infinite loading screen after clicking 'Launch'
- The game servers may be overloaded, especially after a new release.
- If launching the game for the first time with a webcam plugged in, try unplugging the webcam, relaunching, then connecting it.


## Game hangs at loading screen after clicking 'Launch'
- If using a webcam, make sure V4L is installed (video 4 linux, package names may be similar to `v4l-utils`). If using V4L2 Loopback, try removing any loopback devices you have created.


## Black or white RSI Launcher window
- Try editing the [launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) to add the RSI Launcher flag `--in-process-gpu`. For example:
  ```
    "$wine_path"/wine "C:\Program Files\Roberts Space Industries\RSI Launcher\RSI Launcher.exe" --in-process-gpu > "$launch_log" 2>&1
  ```


## Black game window after clicking 'Launch'
- Check our [latest news](/#news) for gpu driver issues or temporary workarounds.
- Contribute to [STARC-197175](https://issue-council.robertsspaceindustries.com/projects/STAR-CITIZEN/issues/STARC-197175) (public) and [STARC-189885](https://issue-council.robertsspaceindustries.com/projects/STAR-CITIZEN/issues/STARC-189885) (evocati only), then use the [LUG Helper](/Tips-and-Tricks#how-to-run-the-lug-helper) to switch to a `LUG Experimental` Wine runner.
- If using DX11 instead of Vulkan, make sure DXVK is [installed and up to date](/Tips-and-Tricks#updating-dxvk-within-a-wine-prefix).
- If using Vulkan, you may need to revert to DX11 by creating a [USER.cfg](/Tips-and-Tricks#usercfg) file.
- If using lsfg-vk for frame gen, use LUG Wine Experimental or revert to DX11.
- If using gamescope, you may need to disable it or double check your configuration.


## Blackout or black screen on Vulkan when flying/boosting/braking/damaged
- Contribute to [STARC-179339](https://issue-council.robertsspaceindustries.com/projects/STAR-CITIZEN/issues/STARC-179339), then use the [LUG Helper](/Tips-and-Tricks#how-to-run-the-lug-helper) to switch to LUG Wine >= 11.5
- If that doesn't work, try a LUG Experimental wine runner.


## Laggy game when using Picom or Compton Compositors
- If you use the Picom or Compton compositor, it may cause a laggy experience despite having high framerates. We recommend disabling the compositor.
