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
- Wine 9.4 to 10.0 from your package manager
- [RawFox](https://github.com/starcitizen-lug/raw-wine/releases)
  - Managed by the LUG Helper
  - v10.3+ are patched to accomodate easy anti-cheat
- [Kron4ek](https://github.com/Kron4ek/Wine-Builds/releases)
  - Managed by the LUG Helper
  - These are prebuilt releases from the [TKG](https://github.com/Frogging-Family/wine-tkg-git) build system
  - v10.3+ are patched to accomodate easy anti-cheat
- [Mactan](https://github.com/mactan-sc/mactan-sc-wine/releases)
  - Managed by the LUG Helper
  - TKG builds with LUG community patches
    - Runners 10.3+ are patched accomodate easy anti-cheat
    - Includes workaround to avoid repeated 30k when loading into the PU
    - Includes NTSync

## Add a Wine runner
To add a custom wine runner
  - Extract the archive to your runners folder. Restart your game launcher after adding a runner and toggle on [CLI mode](Troubleshooting#rsi-launcher-v162-javascript-error)
    - Heroic: `~/.config/heroic/tools/wine/`
    - Heroic flatpak: `~/.var/app/com.heroicgameslauncher.hgl/config/heroic/tools/wine/`
    - Lutris: `~/.local/share/lutris/runners/wine/`
    - Lutris flatpak: `/.var/app/net.lutris.Lutris/data/lutris/runners/wine/`
    - Wine: `~/Games/star-citizen/runners`
  - Edit sc-launch.sh to use the runner or select the runner in your game launcher's configuration
    ```
     ################################################################
     # Configure the wine binaries to be used
     #
     # To use a custom wine runner, set the path to its bin directory
     # export wine_path="/path/to/custom/runner/bin"
     ################################################################
     export wine_path="/home/you-username-goes-here/Games/star-citizen/runners/wine-tkg-ntsync-git-10.3.r0.g3364df08cb6-327-x86_64/bin"
    ```

## Updating DXVK Within a Wine Prefix
Use the LUG Helper tool's `Update DXVK` button

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

## RSI Launcher 2.0
- Requires standard Wine 9.4+ or Proton GE 9-13+ runner
  - Recent Wine versions can be easily installed using the [LUG Helper](https://github.com/starcitizen-lug/lug-helper)
- Remove any `powershell.exe` dll override
- If using standard Wine, winetricks **20250102** or newer is required to install powershell
  1. navigate to your game prefix directory `~/Games/star-citizen`
  2. Use the LUG Helper's Maintence menu `Install Powershell` button
- The 2.0 Launcher may need to be installed manually. See [below](#rsi-launcher-manual-update) for instructions


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
2. Using the [LUG Helper](https://github.com/starcitizen-lug/lug-helper), install a [recommended runner](#recommended-runners). 
3. Remove all EAC workarounds:
    1. Use the LUG Helper Maintenance menu option to "Edit launch script". Remove the EAC environment variable line: `EOS_USE_ANTICHEATCLIENTNULL=1`
    2. In the RSI Launcher, navigate to `Settings -> Games -> LIVE -> Game Location`. If you previously manually applied the Z:\ path workaround, restore the game location to its default C:\ path:  
       <img width="758" height="322" alt="image" src="https://github.com/user-attachments/assets/0ac1ed3a-4c3c-43b9-b93a-a4865e63f784" />
    3. Remove EAC line from `/etc/hosts` file: `127.0.0.1 modules-cdn.eac-prod.on.epicgames.com #Star Citizen EAC workaround`
    4. If you have any other EAC workarounds in place, remove them as well.


## Wayland
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
- Enable HDR with flag `--hdr-enabled`


## How to Run the LUG Helper Script
1. Download the latest [LUG Helper](https://github.com/starcitizen-lug/lug-helper/releases/latest) .tar.gz archive
2. Extract the .tar.gz archive
3. To run `lug-helper.sh` from a terminal (recommended):
    1. Open your terminal and use `cd /path/to/extracted/archive` to navigate to the location
    2. List files with the `ls` command
    3. Once you are in the directory containing the `lug-helper.sh` script, run it by typing `./lug-helper.sh`
4. Alternatively, to run `lug-helper.sh` from your file manager:
    1. Navigate to the extracted archive location
    2. Right click on `lug-helper.sh` and select Run as a Program


## AMD FidelityFX Super Resolution (FSR) upscaling
Use the in-game CIG TSR, AMD FSR, or NVIDIA DLSS options, external tools are not recommended

Set environment variable `WINE_FULLSCREEN_FSR=1`. Then, in the Star Citizen graphics settings, set the game to fullscreen and your desired resolution and it will be FSR scaled up. We recommend restarting the game after changing its resolution for better performance.


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
