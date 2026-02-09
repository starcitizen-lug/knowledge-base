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
- If using the Cosmic DE beta, this is a [known issue](https://github.com/pop-os/cosmic-epoch/issues/2368).
- If using Niri see upstream [xwayland-satellite issue report](https://github.com/Supreeeme/xwayland-satellite/issues/189)
- Workarounds:
  - Try using the [LUG Helper](/Tips-and-Tricks#how-to-run-the-lug-helper)'s  
    `Open Wine prefix configuration` option in the Maintenance menu to turn on virtual desktop mode
  - Try xwayland-run package
    ```
    ############################################################################
    # Launch the game
    ############################################################################
    xwayland-run -- "$wine_path"/wine "C:\Program Files\Roberts Space Industries\RSI Launcher\RSI Launcher.exe" > "$launch_log" 2>&1
    ```
  - Try [gamescope](/Tips-and-Tricks#gamescope), or an alternative compositor
  - Try switching to [Experimental Wine Wayland](/Tips-and-Tricks#wine-wayland)


## Launcher indicates You are currently offline
- Log out and back in


## Launch Error - Settings.json not found
- Verify game files


## RSI Launcher Error Code 60101
- [Issue Council LCH-2123](https://issue-council.robertsspaceindustries.com/projects/LAUNCHER/issues/LCH-2123)
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
  ![image](https://user-images.githubusercontent.com/3657071/224719841-ba1e831b-4ace-4f14-b423-3e49528154c6.png)
- Check that the `Vulkan device` is not set to an integrated gpu (ie, Intel)
  - Identify device name using command `vulkaninfo --summary | grep deviceName`
  - Edit the [launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) and set the device name environment variable: `DXVK_FILTER_DEVICE_NAME=yourdevicenamehere`
  - Verify by setting the environment variable `DXVK_HUD=1` and observing the device name in the upper left of the screen
- Also make sure your GPU drivers (Mesa/nvidia) are up to date and DXVK is enabled/updated.
  - Use the LUG Helper to [update dxvk](/Tips-and-Tricks#updating-dxvk-within-a-wine-prefix)
  - For AMD, be sure to use the open source radeon drivers (ie. vulkan-radeon), **not** the proprietary drivers (ie. amdvlk)
- Try switching to a non-staging wine runner from our [recommended runners](/Tips-and-Tricks#recommended-runners) list
- Try [downgrading](/Tips-and-Tricks#updating-dxvk-within-a-wine-prefix) to an older DXVK version


## Failed to initialize dependencies error
- Make sure the `SDL_VIDEODRIVER` environment variable is **NOT** set globally to `wayland` on your system: `env | grep SDL_VIDEODRIVER`
- If it is set, remove it from whichever environment config(s) is setting it.
- [Edit the launch script](#how-to-edit-the-launch-script) and add `unset SDL_VIDEODRIVER` to the environment variables section


## Black or white RSI Launcher window
- Try editing the [launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) to add the RSI Launcher flag `--in-process-gpu`. For example:
  ```
    "$wine_path"/wine "C:\Program Files\Roberts Space Industries\RSI Launcher\RSI Launcher.exe" --in-process-gpu > "$launch_log" 2>&1
  ```


## Black game window after clicking 'Launch'
- Check our [latest news](/#news) for gpu driver issues or temporary workarounds.
- If using DX11 instead of Vulkan, make sure DXVK is [installed and up to date](/Tips-and-Tricks#updating-dxvk-within-a-wine-prefix).
- If using Vulkan, you may need to revert to DX11 by creating a [USER.cfg](/Tips-and-Tricks#usercfg) file.
- If using lsfg-vk for frame gen, it currently does not work with Vulkan. Revert to DX11.
- If using a webcam, make sure V4L is installed (video 4 linux, package names may be similar to `v4l-utils`). If using V4L2 Loopback, try removing any loopback devices you have created.


## Blackout or black screen on Vulkan when flying/boosting/braking/damaged
1. Set the game to fullscreen in the settings.
2. Create a [USER.cfg](/Tips-and-Tricks#usercfg) file and attempt to set `r_height`, `r_width`, or both to be +/- 2 pixels (ex. for 1920x1080, set `r_height` to 1082 or 1078).
3. If that doesn't work, also edit `Height`/`Width` in your attributes.xml file. Use the LUG Helper to [locate your LIVE directory](/Tips-and-Tricks#where-is-my-wine-prefix-where-is-my-liveptu-directory), then navigate to and edit  
   `.../LIVE/user/client/0/Profiles/default/attributes.xml`


## Laggy game when using Picom or Compton Compositors
- If you use the Picom or Compton compositor, it may cause a laggy experience despite having high framerates. We recommend disabling the compositor.
