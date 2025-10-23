---
title: "🖱️ Mouse & Keyboard Issues"
description: "Known issues that can cause unexpected mouse or keyboard behavior in Star Citizen on Linux + troubleshooting steps to resolve them"
parent: "Troubleshooting"
nav_order: 3
---

# 🖱️ Mouse & Keyboard Issues

## Mouse/Cursor warp issues and view snapping in interaction mode
*This issue can also manifest as some main menu buttons not working due to the cursor actually being offset*

Switch to the game's software cursor. Create a user.cfg file in the LIVE, PTU, EPTU, TECH-PREVIEW directory with the following contents:
 ```
   #use software cursor
   pl_pit.forceSoftwareCursor = 1
 ```
Alternatively, you may choose Xorg at your login screen instead of Wayland session.
Other potential workarounds:
- Use LUG Wine 10.15-1 or newer with the game's borderless windowed mode
- LUG Wine Wayland helps mitigate this for some, but note that it's still experimental and YMMV
  - Add environment variable `DISPLAY=` to unset it to empty
  - Add RSI Launcher.exe argument ` --in-process-gpu`
- [Proton](/Alternative-Installations#proton-installation) helps mitigate this for some
- Gamescope helps mitigate this for sonav_order: 3me
  - **Note for Nvidia users:** Gamescope may not work on your hardware. See [a possible fix](nvidia#gamescope-not-working)
  - Install and enable gamescope. Set these options for your display resolution  
  `-W 2560 -H 1440 --force-grab-cursor`
  - Other Gamescope settings that may be required depending on your system: `Window Mode` set to `Fullscreen` if it doesn't launch fullscreen, `-g` in `Custom Settings` to grab keyboard

- Switching to an alternate desktop environment may help; most Gnome users don't seem to experience this issue
- You may try building xwayland with [this patch](https://github.com/Nobara-Project/rpm-sources/blob/main/baseos/xorg-x11-server-Xwayland/xwayland-pointer-warp-fix.patch) applied. If using KDE and patching xwayland, you will also need to install Gamescope and use the `--force-grab-cursor` option


## Mouse/Cursor restricted to a region smaller than the display, or clicks offset from cursor
- Create a user.cfg file in the LIVE, PTU, EPTU, TECH-PREVIEW directory
 ```
 #set to your display resolution) tech support
 r_width = 3440
 r_height = 1440
 ```
- Hyprland users: Try using the in-game fullscreen option instead of the Hyprland equivalent.


## Mouse cursor escaping the game window
- Opening and closing game menu with the escape key usually recaptures the mouse
- You may also try adding a registry key to your Wine prefix:
   - Use the `sc-launch.sh` launch script to open a [Wine maintenance shell](/Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) then run:
     ```
     wine reg add 'HKEY_CURRENT_USER\Software\Wine\X11 Driver' /t REG_SZ /v UseTakeFocus /d N /f
     ```
     Note: If using a third party launcher instead of the native Wine install, you'll need to prepend `WINEPREFIX=/path/to/prefix` before the above command.


## Non-US keyboard keys not working
1. Use the LUG Helper to [switch to a wine](/Tips-and-Tricks#how-to-add-a-wine-runner) with **staging** in the name
2. Use the LUG Helper Maintenance menu `Open Wine prefix configuration` button to run winecfg
3. In the Input tab->Keyboard Settings, select your language from the list
4. Keyboard scancode auto-detection may have to be enabled or disabled depending on your hardware. Try both.
 ![staging_input_menu](https://github.com/user-attachments/assets/94908f79-682d-42ac-89fc-4564f09c3b7c)
5. If the above doesn't work, use the Lug Helper to [edit your launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) to set the `export LANG=` environment variable. You may need to switch to a staging runner besides LUG-Wine.
    ```
    ################################################################
    # Configure the environment
    # Add additional environment variables here as needed
    ################################################################
    export LANG=de_DE
    ```

