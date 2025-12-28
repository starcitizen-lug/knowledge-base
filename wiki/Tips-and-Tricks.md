---
title: "Tips and Tricks"
description: "Recommended distros, wine runners, LUG Helper tips, and other tricks for running Star Citizen on Linux!"
nav_order: 5
---

# Tips and Tricks

## Recommended Distros
We strongly recommend choosing a distro that has up-to-date packages and a solid maintenance reputation.  

- ⭐ Fedora
- Arch
- EndeavourOS *(Arch-based, easier installation)*
- openSUSE Tumbleweed
- ⭐ Bazzite *(see note below)*
- Ubuntu *(only the [latest release](https://en.wikipedia.org/wiki/Ubuntu#Releases))*
- Debian Testing
- Gentoo

{: .note-title }
> Immutable Distros (ie. Bazzite)
> 
> Some immutable distros such as Bazzite come pre-configured with packages that can make it easier to get up and running (ie. Nvidia drivers). While initial setup may be much simpler, they generally limit your ability to tweak and customize the way the system operates. Installing software that isn't already packaged for the OS can also be challenging.
> 
> A distro like Bazzite can be a good choice for Penguins who don't need to tweak things beyond the default install, but be aware of its limitations.

### Not recommended
- Debian Stable
- Ubuntu LTS
- Mint (based on Ubuntu LTS)
- Pop!_OS (based on Ubuntu LTS)
- Zorin (based on Ubuntu LTS)
- Drauger OS
- openSUSE Leap
- Manjaro

{: .caution-title }
> LTS Distros
> 
> LTS releases and out of date distros will likely require extra knowledge and effort to get Star Citizen running. Note that LTS ≠ stable in the traditional sense. LTS distros typically lock their packages to specific major versions which then only receive security updates. This is great for servers but problematic for gaming where new drivers, features, and fixes are important.

{: .caution-title }
> Gaming Distros
> 
> We do not recommend most gaming-focused distributions as many of our Penguins have had issues getting Star Citizen to run. They generally have only an individual or a very small team backing them and, at least where Star Citizen is concerned, don't offer much benefit beyond our recommended distros for most Penguins.


## Recommended Runners
- [LUG-Wine](https://github.com/starcitizen-lug/lug-wine/releases)
  - Default runner in the [LUG Helper](#how-to-run-the-lug-helper)
  - [TKG](https://github.com/Frogging-Family/wine-tkg-git) Builds with LUG patches specifically for Star Citizen
    - lug-wine-tkg-git  
      Standard Wine built for maximum compatibility
    - lug-wine-tkg-staging-git  
      Wine plus experimental [staging patches](https://gitlab.winehq.org/wine/wine-staging)
- [RawFox](https://github.com/starcitizen-lug/raw-wine/releases)
  - Managed by the [LUG Helper](#how-to-run-the-lug-helper)
- [Mactan](https://github.com/mactan-sc/mactan-sc-wine/releases)
  - Managed by the [LUG Helper](#how-to-run-the-lug-helper)
  - [TKG](https://github.com/Frogging-Family/wine-tkg-git) builds with LUG community patches
  - Experimental wine wayland patches


## How to add a Wine runner
- Select the option to "Manage Wine runners" in the [LUG Helper](#how-to-run-the-lug-helper) and it will handle it for you.
- Alternatively, to manually add a custom wine runner:
  - Extract the archive to your runners folder. Restart your game launcher
    - Heroic: `~/.config/heroic/tools/wine/`
    - Heroic flatpak: `~/.var/app/com.heroicgameslauncher.hgl/config/heroic/tools/wine/`
    - Wine: `~/Games/star-citizen/runners`
  - Use the LUG Helper maintenance menu to edit sc-launch.sh to use the runner
    ```
     ################################################################
     # Configure the wine binaries to be used
     #
     # To use a custom wine runner, set the path to its bin directory
     # export wine_path="/path/to/custom/runner/bin"
     ################################################################
     export wine_path="/home/you-username-goes-here/Games/star-citizen/runners/wine-tkg-ntsync-git-10.3.r0.g3364df08cb6-327-x86_64/bin"
    ```


## How to Run the LUG Helper
1. Download the latest [LUG Helper](https://github.com/starcitizen-lug/lug-helper/releases/latest) .tar.gz archive
2. Extract the .tar.gz archive
3. To run `lug-helper.sh` from a terminal (recommended):
    1. Open your terminal and use `cd /path/to/extracted/archive` to navigate to the location
    2. List files with the `ls` command
    3. Once you are in the directory containing the `lug-helper.sh` script, run it by typing
       ```
       ./lug-helper.sh
       ```
4. Alternatively, to run `lug-helper.sh` from your file manager:
    1. Navigate to the extracted archive location
    2. Right click on `lug-helper.sh` and select Run as a Program

{: .tip }
> The Helper uses Zenity for its optional GUI. If you don't see the GUI and want it, install Zenity from your package manager.


## How to edit the launch script
1. Run the [LUG Helper](#how-to-run-the-lug-helper) and select the `Maintenance and Troubleshooting` menu
2. Choose the option to `Edit launch script`  
   ![Edit launch script](https://github.com/user-attachments/assets/6f30b732-3406-4c59-b23b-32bbccacc5ae){: style="display: block;max-height: 350px;" }
3. Alternatively, locate the `sc-launch.sh` file in your Wine prefix directory (by default, `~/Games/star-citizen/sc-launch.sh`) and open it for editing.


## How to update the launch script
1. Run the [LUG Helper](#how-to-run-the-lug-helper) and select the `Maintenance and Troubleshooting` menu
2. Choose the option to `Update launch script`
   ![Update launch script](https://github.com/user-attachments/assets/e0925912-1c89-4eb2-9dae-5dbd3fe9806e){: style="display: block;max-height: 300px;" }


## How to get a Wine maintenance shell using the launch script
1. In a terminal, navigate to your Star Citizen wine prefix directory. By default, this is `~/Games/star-citizen`
2. Verify that `sc-launch.sh` exists.
3. Run `./sc-launch.sh shell` to enter a prepared shell environment for your prefix. All Wine prefix environment variables will be set for you.
4. Type `exit` when done.


## Where is my Wine prefix? Where is my LIVE/PTU directory?
1. Run the [LUG Helper](#how-to-run-the-lug-helper) and select the `Maintenance and Troubleshooting` menu.
2. Select the `Display Helper and Star Citizen directories` option.
3. Click on the relevant path to open it in your file manager.

{: .tip-title }
>
> LIVE/PTU Directory
> 
> Click the `Star Citizen game directory` link to access your LIVE/PTU directory. By default, this will open:
> `~/Games/star-citizen/drive_c/Program Files/Roberts Space Industries/StarCitizen`


## Updating DXVK Within a Wine Prefix
Use the [LUG Helper's](#how-to-run-the-lug-helper) `Manage DXVK` button

**To downgrade dxvk to a previous version:**
1. Enter a [Wine maintenance shell](Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) for your prefix using the `sc-launch.sh` script.
3. Run `winetricks`
4. Click "Select the default wineprefix" (verify that the file path in the title bar is your star-citizen game)
5. Click "Install a Windows DLL or component"
6. Select an older dxvk such as dxvk 2.6.1 or older and click OK


## RSI Launcher Manual Update
1. Using the latest [LUG Helper](https://wiki.starcitizen-lug.org/Tips-and-Tricks#how-to-run-the-lug-helper), select `Maintenance and Troubleshooting` then choose `Update/Re-install RSI Launcher`.


## Console Variables
Below are some useful console variables. Tap the grave/backtick/tilde key (above tab) to open the console. See our troubleshooting page for [non-US keyboards](Troubleshooting/mouse-keyboard-issues#non-us-keyboard-keys-not-working) if you have trouble opening the console.
- `r_displayinfo` [ 1, 2, 3, 0 ]
  - show fps and other details
- `r_displaysessioninfo` [ 1, 0 ] 
  - show session info QR code for reporting
- `r_displayframegraph` [ 1, 0 ]
  - show chart of frame time
  - MT (main thread)
  - RT (render thread)
- `pl_pit.forceSoftwareCursor` [ 1, 0 ]
  - force software cursor 


## USER.cfg
Varibles set using the in-game console must be reapplied each session. Create a USER.cfg file to apply the changes automatically each session.
1. Use the LUG Helper to [open your Star Citizen LIVE directory](/Tips-and-Tricks#where-is-my-wine-prefix-where-is-my-liveptu-directory)
2. Create a file named `USER.cfg` in your LIVE directory
3. Copy the text block below into it
4. Uncomment any variables and configure as needed
5. Save then launch the game as normal. Any changes will be automatically applied  

```
# Set to your display resolution
# r_width = 1920
# r_height = 1080

# Enable software cursor to workaround cursor warping
# pl_pit.forceSoftwareCursor = 1

# Enable borderless windowed mode
# r_WindowMode = 2

# Force game renderer - 0 = DX11, 1 = Vulkan
# r.graphicsRenderer = 0

# Enable in-game performance HUD
# r_displayinfo = 1

# Limit frame rate
# sys_MaxFPS = 120
# sys_MaxIdleFPS = 120

# Toggle vsync
# r_VSync = 0

# Disable Temporal Super Resolution and all anti-aliasing
# r.TSR = 0
```


## Easy Anti-Cheat

{: .important-title }
>
> Check the [latest news](/#news) for any changes
>
> Refer to the [Easy Anti-Cheat](Troubleshooting/easy-anti-cheat) page for troubleshooting steps


## Wine Wayland

{: .warning }
> If the `Launch Game` button is unclickable in the launcher, or mouse clicks are not working in settings, the buttons may be offset. Resize the window to reset them, or use `Tab`/`Shift+Tab` and `Enter` to interact with them.
> 
> Turn off any virtual keyboard. These conflict with the `F` interaction key and make the inner-thought menu appear to flicker.

- Experimental Wine Wayland
  - Use the [LUG Helper](#how-to-run-the-lug-helper) to select lug-wine 11.0-rc1-2 or newer
  - Edit the [launch script](#how-to-edit-the-launch-script) to add environment variable `export DISPLAY=` to unset it to empty
  - If you experience a white or black launcher add this [RSI Launcher.exe argument](/Troubleshooting/unexpected-behavior#launcher-white-or-black-screen)
- Experimental Proton Wayland (for proton runners)
  - Add environment variable `PROTON_ENABLE_WAYLAND=1`
 
- Set primary monitor, Edit the [launch script](#how-to-edit-the-launch-script) to add environment variable `WAYLANDDRV_PRIMARY_MONITOR` Replace the value for your monitor DP-1, DP-2, HDMI-A-1, etc  
    `export WAYLANDDRV_PRIMARY_MONITOR=DP-1`  

- Set resolution with [USER.cfg](Tips-and-Tricks#usercfg)

- Set DPI with [LUG Helper](#how-to-run-the-lug-helper) Maintenance menu > Edit wine prefix configuration
 
## HDR (High Dynamic Range)
CIG's vulkan doesn't have HDR yet

Requires experimental native [Wayland](Tips-and-Tricks#wine-wayland) or [Gamescope](Tips-and-Tricks#gamescope)

To enable HDR in native Wayland:

Run `wayland-info|grep color` in a terminal, if you **do not** see `wp_color_manager_v1` or if you use an Nvidia gpu then you will need to install [VK_hdr_layer](https://github.com/Zamundaaa/VK_hdr_layer) and add environment variable `ENABLE_HDR_WSI=1`
- Wine
  - Add environment variable  `DXVK_HDR=1`
- Proton (GE-Proton10-1 or newer)
  - Add environment variable `PROTON_ENABLE_HDR=1`


## Gamescope
- Use the LUG Helper to [edit your launch script](#how-to-edit-the-launch-script)
- Prepend your gamescope arguments to the launch line at the bottom of the launch script. For example:
  ```
  gamescope --hdr-enabled -W 2560 -H 1440 --force-grab-cursor -- "$wine_path"/wine "C:\Program Files\Roberts Space Industries\RSI Launcher\RSI Launcher.exe" > "$launch_log" 2>&1
  ```
- Enable HDR with flag `--hdr-enabled`
 

## Hide RSI Launcher Tray Icon
- Enter a [Wine maintenance shell](Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script)
  Use `wine regedit` GUI to add registry key and DWORD value 1
  `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`  
  `NoTrayItemsDisplay` = 1

## Pre-launch and Post-exit Scripts
The [launch script](#how-to-edit-the-launch-script) installed by the LUG Helper can be modified to run pre-launch and post-exit scripts. These scripts can be used to launch utilities like antimicrox, opentrack, etc., or disable/re-enable mouse acceleration for more precise FPS handling.

This can be inserted into the launch script above the "Launch the game" section:  
_sc-launch.sh_
```bash
#############################################
# Run optional prelaunch and postexit scripts
#############################################
# To use create the scripts with your desired actions in them and
# place them in your prefix directory: sc-prelaunch.sh and sc-postexit.sh

# Run the prelaunch script
"$WINEPREFIX/sc-prelaunch.sh"

# Run the post-exit script on exit
trap "\"$WINEPREFIX\"/sc-postexit.sh" EXIT
```

Some example pre/post launch scripts:

_sc-prelaunch.sh_
```bash
#!/bin/bash
## Disable Mouse Acceleration

## GNOME
# gsettings set org.gnome.desktop.peripherals.mouse accel-profile flat

## KDE
# kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" true
```

_sc-postexit.sh_
```bash
#!/bin/bash
## Reset Mouse Acceleration

## Gnome
# gsettings set org.gnome.desktop.peripherals.mouse accel-profile default

## KDE
# kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" false
```
