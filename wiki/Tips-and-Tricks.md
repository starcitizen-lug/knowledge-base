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
> Some immutable distros such as Bazzite come pre-configured with packages that can make it easier to get up and running (nVidia drivers). While initial setup may be much simpler, they generally limit your ability to tweak and customize the way the system operates. Installing software that isn't already packaged for the OS can also be challenging.
> 
> A distro like Bazzite can be a good choice for Penguins who don't need to tweak things beyond the default install, but be aware of its limitations.

### Not recommended
- Debian Stable
- Ubuntu LTS
- Mint (based on Ubuntu LTS)
- Pop!_OS (based on Ubuntu LTS)
- Zorin (based on very old Ubuntu LTS)
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
  - TKG Builds with LUG patches specifically for Star Citizen
    - lug-wine-tkg-fsync-git  
      Standard Wine built for maximum compatibility. Works with glibc as old as v2.31
    - lug-wine-tkg-ntsync-git  
      NTSync patched Wine. Requires linux kernel 6.14+ and glibc >=2.38
    - lug-wine-tkg-staging-fsync-git  
      Wine plus experimental staging patches. Works with glibc as old as v2.31
    - lug-wine-tkg-staging-ntsync-git  
      NTSync patched Wine plus experimental staging patches. Requires linux kernel 6.14+ and glibc >=2.38
- [Mactan](https://github.com/mactan-sc/mactan-sc-wine/releases)
  - Managed by the [LUG Helper](#how-to-run-the-lug-helper)
  - TKG builds with LUG community patches
  - Experimental wine wayland patches
- [RawFox](https://github.com/starcitizen-lug/raw-wine/releases)
  - Managed by the [LUG Helper](#how-to-run-the-lug-helper)
  - Recommend v10.0 as of 7-25 its unpatched and works with the C:\ path and enabled EAC


## How to add a Wine runner
- Select the option to "Manage Wine runners" in the [LUG Helper](#how-to-run-the-lug-helper) and it will handle it for you.
- Alternatively, to manually add a custom wine runner:
  - Extract the archive to your runners folder. Restart your game launcher after adding a runner and toggle on [CLI mode](Troubleshooting/lutris#rsi-launcher-v162-javascript-error)
    - Heroic: `~/.config/heroic/tools/wine/`
    - Heroic flatpak: `~/.var/app/com.heroicgameslauncher.hgl/config/heroic/tools/wine/`
    - Lutris: `~/.local/share/lutris/runners/wine/`
    - Lutris flatpak: `/.var/app/net.lutris.Lutris/data/lutris/runners/wine/`
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


## Updating DXVK Within a Wine Prefix
Use the [LUG Helper](#how-to-run-the-lug-helper) tool's `Update DXVK` button

**To downgrade dxvk to a previous version:**
1. Enter a [Wine maintenance shell](Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) for your prefix using the `sc-launch.sh` script.
3. Run `winetricks`
4. Click "Select the default wineprefix" (verify that the file path in the title bar is your star-citizen game)
5. Click "Install a Windows DLL or component"
6. Select an older dxvk such as dxvk 2.6.1 or older and click OK


## NixOS
On NixOS, to set `vm.max_map_count` and `fs.file-max`, add the following to your NixOS config:

```nix
# ... your NixOS Config ...
boot.kernel.sysctl = {
  "vm.max_map_count" = 16777216;
  "fs.file-max" = 524288;
};
```

Custom wine runners will not work out of the box if the system wine install does not work ( `wineWow64Packages.stableFull` recommended) try `wine-astral` from [nix-citizen](https://github.com/LovingMelody/nix-citizen) or one of the [Alternative Installation](Alternative-Installations#nix-installation) methods.



## RSI Launcher Manual Update
1. Download the [latest](https://robertsspaceindustries.com/download) RSI Launcher installer
2. Enter a [Wine maintenance shell](Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) for your prefix using the `sc-launch.sh` script.
3. Then, run the following command (be sure to type the correct download path):
    ```
    WINEDLLOVERRIDES="dxwebsetup.exe,dotNetFx45_Full_setup.exe=d" wine "/path/to/downloaded/RSI Launcher-Setup-2.6.0.exe" /S
    ```


## Console Variables
- r_displayinfo [ 1, 2, 3, 0 ]
  - show fps and other details
- r_displaysessioninfo [ 1, 0 ] 
  - show session info QR code for reporting
- r_displayframegraph [ 1, 0 ]
  - show chart of frame time
  - MT (main thread)
  - RT (render thread)
- pl_pit.forceSoftwareCursor [ 1, 0 ]
  - force software cursor 


## USER.cfg
```
# set to your display resolution
# r_width = 1920
# r_height = 1080

#use software cursor
pl_pit.forceSoftwareCursor = 1

# set borderless
# r_WindowMode = 2

# 0 = DX11, 1 = Vulkan
# r.graphicsRenderer = 0

# r_displayinfo = 1

# sys_MaxFPS = 120
# sysmaxidleFPS = 120

# r_VSync = 0
```


## Easy Anti-Cheat

{: .important-title }
>
> Check the [latest news](/#general-news) for any wine changes

1. Use RSI Launcher 2.5.1 or newer
2. Ensure there are no symlinks or special characters in the path to your Wine prefix
3. Use the latest [LUG Helper](#how-to-add-a-wine-runner) to switch to a LUG-Wine runner
4. [Update your launch script](#how-to-update-the-launch-script)
5. Remove any EAC workarounds by [editing your launch script](#how-to-edit-the-launch-script) or your game launcher settings, check for each one to see if it exists
    - Remove Environment variable `EOS_USE_ANTICHEATCLIENTNULL=1`
    - Remove Hosts entry in file named `/etc/hosts` with the value
      ```
      127.0.0.1 modules-cdn.eac-prod.on.epicgames.com #Star Citizen EAC workaround
      ```
    - In the RSI Launcher, navigate to `Settings -> Games -> LIVE -> Game Location`. If you previously used the Z:\ path workaround, put it back to the default C:\ path  
       ![Game path in launcher](https://github.com/user-attachments/assets/0ac1ed3a-4c3c-43b9-b93a-a4865e63f784){: style="display: block;max-height: 250px;" }  


## Wine Wayland

{: .note }
> RSI Launcher buttons may be offset, resize the window or use tab/shift+tab controls for the launcher

- Experimental Wine Wayland
  - Use a Wine without **staging** in the name
  - Edit the [launch script](#how-to-edit-the-launch-script) to add environment variable `export DISPLAY=` to unset it to empty
  - Add RSI Launcher.exe argument `--in-process-gpu` example:
    ```
    "$wine_path"/wine "C:\Program Files\Roberts Space Industries\RSI Launcher\RSI Launcher.exe" --in-process-gpu > "$launch_log" 2>&1
    ```
- Experimental Proton Wayland
  - Add environment variable `PROTON_ENABLE_WAYLAND=1`
  - Add RSI Launcher.exe argument ` --in-process-gpu`
 
## HDR (High Dynamic Range)
CIG's vulkan doesn't have HDR yet

Requires experimental native [Wayland](Tips-and-Tricks#wine-wayland) or [Gamescope](Tips-and-Tricks#gamescope)

To enable HDR in native Wayland:

Run `wayland-info|grep color` in a terminal, if you **do not** see `wp_color_manager_v1` then you will need to install [VK_hdr_layer](https://github.com/Zamundaaa/VK_hdr_layer) and add environment variable `ENABLE_HDR_WSI=1`
- Wine
  - Add environment variable  `DXVK_HDR=1`
- Proton (GE-Proton10-1 or newer)
  - Add environment variable `PROTON_ENABLE_HDR=1`


## Gamescope
- Use the LUG Helper to [edit your launch script](#how-to-edit-the-launch-script)
- Prepend your gamescope arguments to the launch line at the bottom of the launch script. For example:
  ```
  gamescope --hdr-enabled -W 2560 -H 1440 --force-grab-cursor "$wine_path"/wine "C:\Program Files\Roberts Space Industries\RSI Launcher\RSI Launcher.exe" > "$launch_log" 2>&1
  ```
- Enable HDR with flag `--hdr-enabled`


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
