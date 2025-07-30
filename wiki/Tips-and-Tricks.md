## Recommended Distros
We strongly recommend choosing a distro that has up-to-date packages and a solid maintenance reputation.  

The following distributions make our 👍 list and generally work well with Star Citizen:
- Arch
- EndeavourOS (Arch-based)
- Fedora
- openSUSE Tumbleweed
- Debian Testing
- Ubuntu (*only the latest non-LTS release*)
- Gentoo


The following distributions make our 👎 list and generally pose additional challenges:
- Debian Stable
- Ubuntu LTS
- Mint (based on Ubuntu LTS)
- Pop!_OS (based on Ubuntu LTS)
- Drauger OS
- openSUSE Leap
- Manjaro

We do not recommend 👎 LTS distros. *LTS releases and out of date distros are likely to cause many headaches.* LTS ≠ stable. LTS just means old packages locked to a specific major version which only receive security updates. This is great for servers but terrible for gaming where new features and fixes are important. #LTSbadjustdontplskthx  

We do not recommend 👎 most gaming-focused distributions as many of our Penguins have had issues installing the required dependencies to make Star Citizen run. They generally have only an individual or a very small team backing them and, at least where Star Citizen is concerned, do not live up to the promise.  We especially suggest avoiding Pop!_OS and Drauger OS due to irresolvable compatibility issues

Other distributions we suggest avoiding 👎 due to frequent package incompatibilities, old dependencies, and update issues are: Manjaro, Ubuntu LTS, Mint (based on Ubuntu LTS), Debian Stable, and openSUSE Leap.

If you're new to Linux, we recommend avoiding immutable distros such as Bazzite, Nix, Silverblue, Universal Blue, etc for now; they come with a steeper learning curve and are better suited to those with more experience.


## Recommended Runners
- [LUG-Wine](https://github.com/starcitizen-lug/lug-wine/releases)
  - Default runner in the [LUG Helper](#how-to-run-the-lug-helper)
  - TKG Builds with LUG patches specifically for Star Citizen
- [Mactan](https://github.com/mactan-sc/mactan-sc-wine/releases)
  - Managed by the [LUG Helper](#how-to-run-the-lug-helper)
  - TKG builds with LUG community patches
    - Runners 10.3+ are patched accomodate easy anti-cheat
    - Includes workaround to avoid repeated 30k when loading into the PU
    - Includes NTSync
- [RawFox](https://github.com/starcitizen-lug/raw-wine/releases)
  - Managed by the [LUG Helper](#how-to-run-the-lug-helper)
  - recommend v10.0 as of 7-25 its unpatched and works with the C:\ path and enabled EAC


## How to add a Wine runner
- Select the option to "Manage Wine runners" in the [LUG Helper](#how-to-run-the-lug-helper) and it will handle it for you.
- Alternatively, to manually add a custom wine runner:
  - Extract the archive to your runners folder. Restart your game launcher after adding a runner and toggle on [CLI mode](Troubleshooting#rsi-launcher-v162-javascript-error)
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
    3. Once you are in the directory containing the `lug-helper.sh` script, run it by typing `./lug-helper.sh`
4. Alternatively, to run `lug-helper.sh` from your file manager:
    1. Navigate to the extracted archive location
    2. Right click on `lug-helper.sh` and select Run as a Program


## How to edit the launch script
1. Run the [LUG Helper](#how-to-run-the-lug-helper) and select the Maintenance and Troubleshooting menu
2. Choose the option to `Edit launch script`  
   <img height="350" alt="image" src="https://github.com/user-attachments/assets/6f30b732-3406-4c59-b23b-32bbccacc5ae" />
3. Alternatively, locate the `sc-launch.sh` file in your Wine prefix directory (by default, `~/Games/star-citizen/sc-launch.sh`) and open it for editing.


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

Custom wine runners will not work out of the box if the system wine install does not work ( `wineWow64Packages.stableFull` recommended) try `wine-astral` from [nix-citizen](https://github.com/LovingMelody/nix-citizen) or one of the [Alternative Installation](Alternative-Installations##nix-installation) methods.



## RSI Launcher Manual Update
- Download the [latest](https://robertsspaceindustries.com/download) RSI Launcher installer
- Wine:
  - Open a terminal and run `~/Games/star-citizen/sc-launch.sh shell`
  - Then run the following command
    ```
    WINEDLLOVERRIDES="dxwebsetup.exe,dotNetFx45_Full_setup.exe=d" wine ~/path/to/your/installer /S
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


## Proton
- Remove any `powershell.exe` dll override
- Add environment variables:
  - `GAMEID: umu-starcitizen`
  - `PROTONPATH: GE-Proton`


## Easy Anti-Cheat
> [!important]
> Check the [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#general-news) for any wine changes

1. Use RSI Launcher 2.5.1 or newer
2. Use the latest [LUG Helper](https://github.com/starcitizen-lug/lug-helper) to switch to a LUG-Wine runner
3. Remove all old EAC workarounds if you have them:
    1. Use the LUG Helper Maintenance menu option to "Update launch script" to remove the previous environment variable workaround.  
       <img height="300" alt="image" src="https://github.com/user-attachments/assets/e0925912-1c89-4eb2-9dae-5dbd3fe9806e" />  
       Alternatively, select "Edit launch script" and manually remove the EAC environment variable: `EOS_USE_ANTICHEATCLIENTNULL=1`  
    2. If using Lutris or another third party launcher, remove the above EAC environment variable from its settings.
    3. In the RSI Launcher, navigate to `Settings -> Games -> LIVE -> Game Location`. If you previously manually applied the Z:\ path workaround, restore the game location to its default C:\ path:  
       <img height="250" alt="image" src="https://github.com/user-attachments/assets/0ac1ed3a-4c3c-43b9-b93a-a4865e63f784" />
    4. Remove EAC line from `/etc/hosts` file: `127.0.0.1 modules-cdn.eac-prod.on.epicgames.com #Star Citizen EAC workaround`
    5. If you have any other EAC workarounds in place, remove them as well.


## Wine Wayland
- Experimental Wine Wayland (Non-staging Wine 9.22 or newer)
  - Add environment variable `DISPLAY=` to unset it to empty
  - Add RSI Launcher.exe argument ` --in-process-gpu`
- Experimental Proton Wayland (GE-Proton10-1 or newer)
  - Add environment variable `PROTON_ENABLE_WAYLAND=1`
  - Add RSI Launcher.exe argument ` --in-process-gpu`
 
## HDR (High Dynamic Range)
CIG's vulkan doesn't have HDR yet

Requires experimental native [Wayland](Tips-and-Tricks#Wayland) or [Gamescope](Tips-and-Tricks#Gamescope)

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


## Automatically Disable/Re-Enable Mouse Acceleration
Lutris can automatically toggle on/off a flat mouse acceleration profile with the following configuration.

Configure the game within Lutris and go to `System options`. Make sure `Show advanced options` is checked.  
Add the following to the `Pre-launch script` and `Post-exit script` fields.  
Alternatively, see [below](#lutris-pre-launch-and-post-exit-scripts) for a sample script file that incorporates this and other pre-launch tweaks.

**Gnome**

`/usr/bin/sh -c "gsettings set org.gnome.desktop.peripherals.mouse accel-profile flat"`

`/usr/bin/sh -c "gsettings set org.gnome.desktop.peripherals.mouse accel-profile default"`

**KDE**

`/usr/bin/sh -c 'kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" true'`

`/usr/bin/sh -c 'kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" false'`


## Lutris Pre-launch and Post-exit Scripts
Below are sample pre-launch and post-exit scripts that incorporate the mouse acceleration settings [described above](#automatically-disablere-enable-mouse-acceleration).
To use them, create `sc-prelaunch.sh` and `sc-postexit.sh` in your wine prefix, uncomment the appropriate mouse acceleration lines based on your desktop environment, then configure Lutris to use the scripts:
- `Right click the game->Configure->System options` and set `Pre-launch script` to `/path/to/wine/prefix/sc-pre-launch.sh`
- `Right click the game->Configure->System options` and set `Post-exit script` to `/path/to/wine/prefix/sc-post-exit.sh`
- Enable `Wait for pre-launch script completion`

_sc-prelaunch.sh_
```bash
#!/bin/bash
############################################
## Lutris pre-launch script for Star Citizen
############################################

## Disable Mouse Acceleration
## GNOME
#gsettings set org.gnome.desktop.peripherals.mouse accel-profile flat

## KDE
#kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" true

## End Mouse Acceleration
```

_sc-postexit.sh_
```bash
#!/bin/bash
###########################################
## Lutris post-exit script for Star Citizen
###########################################

## Reset Mouse Acceleration
## Gnome
#gsettings set org.gnome.desktop.peripherals.mouse accel-profile default

## KDE
#kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" false

## End Mouse Acceleration
```
