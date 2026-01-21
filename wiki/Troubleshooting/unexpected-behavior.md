---
title: "🤪 Unexpected Behavior"
description: "Known issues that can cause unexpected behavior in Star Citizen on Linux + troubleshooting steps to resolve them"
parent: "Troubleshooting"
nav_order: 4
md_message: "You are viewing raw source files... Go to https://wiki.starcitizen-lug.org/ to use the wiki!"
---

# 🤪 Unexpected Behavior


## Empty launcher
- Try logging out and back in, or reset the launcher by pressing Ctrl+Shift+Alt+R
- Wine v10.17 caused launcher rendering issues. Use the [LUG Helper](/Tips-and-Tricks#how-to-add-a-wine-runner) to install a different LUG-Wine runner version.
- If using the Cosmic DE beta, this is a [known issue](https://github.com/pop-os/cosmic-epoch/issues/2368). Try using the [LUG Helper](/Tips-and-Tricks#how-to-run-the-lug-helper)'s `Open Wine prefix configuration` option in the Maintenance menu to turn on virtual desktop mode.
- Try switching to [Experimental Wayland](/Tips-and-Tricks#wine-wayland)


## Launcher white or black screen
- Edit the [launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) and add RSI Launcher flag `--in-process-gpu` example:
  ```
    "$wine_path"/wine "C:\Program Files\Roberts Space Industries\RSI Launcher\RSI Launcher.exe" --in-process-gpu > "$launch_log" 2>&1
  ```


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

## Required Vulkan Extensions are missing error / poor performance compared to windows / error code 3
- Check if you have amdvlk installed by running `vulkaninfo --summary`. The vulkaninfo utility is part of the package `vulkan-tools` on most distros. You can also check your package manager.
- If your system is using amdvlk, uninstall that package and replace it with `vulkan-radeon`.
- For additional help with this, ask in our [Discord](/) tech support channel.


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


## Black or flickering window, possible crash with errors 15006 or 30007
- Check for larger resolutions and scaling settings.  See CIG's [support article](https://support.robertsspaceindustries.com/hc/en-us/articles/37500283848983-Optimizing-Graphics-Settings)


## Black/transparent window after clicking 'Launch'
- Check our [latest news](/#news) for gpu driver issues, necessary workarounds, and currently recommended runner/DXVK versions.
- Make sure DXVK is installed and enabled

## Launcher crashes/hangs after entering login info when running Niri WM and/or xwayland-satellite
- See [upstream issue report](https://github.com/Supreeeme/xwayland-satellite/issues/189)
- Workarounds: Use xwayland-run, [gamescope](/Tips-and-Tricks#gamescope), an alternative to xwayland-satellite, an alternative compositor, or try switching to [Experimental Wine Wayland](/Tips-and-Tricks#wine-wayland).

## Laggy game when using Picom or Compton Compositors
- If you use the Picom or Compton compositor, it may cause a laggy experience despite having high framerates. We recommend disabling the compositor.
