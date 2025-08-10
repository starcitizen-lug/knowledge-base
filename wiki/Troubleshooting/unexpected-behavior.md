---
title: "🤪 Unexpected Behavior"
parent: "Troubleshooting"
nav_order: 3
---


#### Mouse/Cursor warp issues and view snapping in interaction mode
*This issue can also manifest as some main menu buttons not working due to the cursor actually being offset*

Switch to the game's software cursor. Create a user.cfg file in the LIVE, PTU, EPTU, TECH-PREVIEW directory with the following contents:
 ```
   #use software cursor
   pl_pit.forceSoftwareCursor = 1
 ```
Alternatively, you may choose Xorg at your login screen instead of Wayland session.
Other potential workarounds:
- Non-staging Wine Wayland helps mitigate this for some, but note that it's still experimental and YMMV
  - Add environment variable `DISPLAY=` to unset it to empty
  - Add RSI Launcher.exe argument ` --in-process-gpu`
- [Proton](/Alternative-Installations#proton-installation) helps mitigate this for some
- Gamescope helps mitigate this for sonav_order: 3me
  - **Note for Nvidia users:** Gamescope may not work on your hardware. See [a possible fix below](nvidia#gamescope-not-working)
  - Install and enable gamescope. Set these options for your display resolution `-W 2560 -H 1440 --force-grab-cursor`
  - Other Gamescope settings that may be required depending on your system: `Window Mode` set to `Fullscreen` if it doesn't launch fullscreen, `-g` in `Custom Settings` to grab keyboard

- Switching to an alternate desktop environment may help; most Gnome users don't seem to experience this issue
- You may try building xwayland with [this patch](https://github.com/Nobara-Project/rpm-sources/blob/main/baseos/xorg-x11-server-Xwayland/xwayland-pointer-warp-fix.patch) applied. If using KDE and patching xwayland, you will also need to install Gamescope and use the `--force-grab-cursor` option


#### Mouse/Cursor restricted to a region smaller than the display, or clicks offset from cursor
- Create a user.cfg file in the LIVE, PTU, EPTU, TECH-PREVIEW directory
 ```
 #set to your display resolution) tech support
 r_width = 3440
 r_height = 1440
 ```
- Hyprland users: Try using the in-game fullscreen option instead of the Hyprland equivalent.


#### Mouse cursor escaping the game window
- Toggling the game console with the tilde (`~`) key/the key left of the number `1` usually recaptures the mouse.
- You may also try adding a registry key to your Wine prefix:
   - Use the `sc-launch.sh` launch script to open a [Wine maintenance shell](/Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) then run the following command:
     ```
     wine reg add 'HKEY_CURRENT_USER\Software\Wine\X11 Driver' /t REG_SZ /v UseTakeFocus /d N /f
     ```
     Note: If using a third party launcher instead of the native Wine install, you'll need to prepend `WINEPREFIX=/path/to/prefix` before the above command.


#### Empty launcher
- Log out log back in, or reset the launcher by pressing Ctrl+Shift+Alt+R


#### Visual glitches or semi-transparent lines, poor performance, possibly random crashes
- DXVK may be broken or disabled. Reinstall it using the LUG Helper DXVK and maintenance menus
- Your game shader cache may need to be cleared. Use the Delete Shaders option in the RSI Launcher > Settings > Games > {LIVE,PTU} > Delete Local Settings > Shaders folder


#### Account login failed (possible code 19000)
This is a generic error code representing any issue with logging in to CIG servers
- Expected when attempting launch/login during a patch release
- Kill the launcher and restart it and try again
- Ensure that IPv6 is not disabled

#### Anticheat encountered an error (possible code 30033, 30034)
- Please follow [our EAC migration instructions](/Tips-and-Tricks#easy-anti-cheat)
- Check your process list for any lingering wine processes. Reboot if necessary.
- You may have to delete the EAC directory in youre prefix's `AppData/Roaming` directory.
- You may also have to delete the EAC directory in the Star Citizen `LIVE` directory, followed by verifying files in the launcher.


#### Required Vulkan Extensions are missing error / poor performance compared to windows / error code 3
- Check if you have amdvlk installed by running `vulkaninfo --summary`. The vulkaninfo utility is part of the package `vulkan-tools` on most distros. You can also check your package manager.
- If your system is using amdvlk, uninstall that package and replace it with `vulkan-radeon`.
- For additional help with this, ask in our [Discord](/) tech support channel.


#### DirectX error message
- Error may read "Star Citizen requires DirectX feature level of 11.1 as a minimum which is not supported at present on this machine"  
  ![image](https://user-images.githubusercontent.com/3657071/224719841-ba1e831b-4ace-4f14-b423-3e49528154c6.png)
- Check that the `Vulkan device` is not set to an integrated gpu (ie, Intel)
  - identify device name using command `vulkaninfo --summary | grep deviceName`
  - set device name with environment variable `DXVK_FILTER_DEVICE_NAME=yourdevicenamehere`
  - verify by setting environment variable `DXVK_HUD=1` and observing the device name in the upper left of the screen
- Also make sure your GPU drivers (Mesa/nvidia) are up to date and DXVK is enabled/updated.
  - Use the LUG Helper to update dxvk
  - For AMD, be sure to use the open source radeon drivers (ie. vulkan-radeon), **not** the proprietary drivers (ie. amdvlk)
- Try switching to a non-staging wine runner from our [recommended runners](/Tips-and-Tricks#recommended-runners) list
- Try [downgrading](/Tips-and-Tricks#updating-dxvk-within-a-wine-prefix) to an older DXVK version


#### Failed to initialize dependencies error
- Make sure the `SDL_VIDEODRIVER` environment variable is **NOT** set globally to `wayland` on your system: `env | grep SDL_VIDEODRIVER`
- If it is set, remove it from whichever environment config(s) is setting it.


#### Black or flickering window, possible crash with errors 15006 or 30007
- Check for larger resolutions and scaling settings.  See CIG's [support article](https://support.robertsspaceindustries.com/hc/en-us/articles/360000081887-Guide-to-Graphic-Issues#large-res)


#### Black/transparent window after clicking 'Launch'
- Check our [latest news](/#news) for gpu driver issues, necessary workarounds, and currently recommended runner/DXVK versions.
- Make sure DXVK is installed and enabled


#### Launcher crashes/hangs after entering login info when running Niri WM and/or xwayland-satellite
- See [upstream issue report](https://github.com/Supreeeme/xwayland-satellite/issues/189)
- Workarounds: Use xwayland-run, [gamescope](/Tips-and-Tricks#gamescope), an alternative to xwayland-satellite, or an alternative compositor.


#### Non-US keyboard keys not working
1. Use the Lug Helper maintenance menu to edit the launch script to set the `export LANG=` environment variable. For example:
    ```
    ################################################################
    # Configure the environment
    # Add additional environment variables here as needed
    ################################################################
    export LANG=de_DE
    ```
3. Use the LUG Helper's `Manage Runners` option to select a wine with **staging** in the name. Check the [latest news](/#general-news) for wine info 
4. Use the LUG Helper Maintenance menu `Open Wine prefix configuration` button to run winecfg
5. Select your language from the list and enable scancode auto-detection
 ![staging_input_menu](https://github.com/user-attachments/assets/94908f79-682d-42ac-89fc-4564f09c3b7c)

