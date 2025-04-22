## Recommended Distros
We strongly recommend choosing a distro that has up-to-date packages and a solid maintenance reputation.  

The following distributions make our 👍 list and generally work well with Star Citizen:
- Arch
- EndeavourOS (Arch-based)
- Fedora
- openSUSE Tumbleweed
- Debian Testing
- Ubuntu *(only the latest non-LTS release)*
- Gentoo

We do not recommend 👎 LTS distros. *LTS releases and out of date distros are likely to cause many headaches.* LTS ≠ stable. LTS just means old packages locked to a specific major version which only receive security updates. This is great for servers but terrible for gaming where new features and fixes are important. #LTSbadjustdontplskthx  

We do not recommend 👎 most gaming-focused distributions as many of our Penguins have had issues installing the required dependencies to make Star Citizen run. They generally have only an individual or a very small team backing them and, at least where Star Citizen is concerned, do not live up to the promise.  
- We especially suggest avoiding Pop!_OS and Drauger OS due to irresolvable compatibility issues

Other distributions we suggest avoiding 👎 due to frequent package incompatibilities, old dependencies, and update issues are: Manjaro, Ubuntu LTS, Mint (based on Ubuntu LTS), Debian Stable, and openSUSE Leap.

If you're new to Linux, we recommend avoiding immutable distros such as Bazzite, Nix, Silverblue, Universal Blue, etc for now; they come with a steeper learning curve and are better suited to those with more experience.


## Recommended Runners
- Wine 9.4 or newer from your package manager
- [RawFox](https://github.com/starcitizen-lug/raw-wine/releases)
  - Managed by the LUG Helper
  - 10.3+ patched to accomodate PTU's easy anti-cheat enforcement
- [Kron4ek](https://github.com/Kron4ek/Wine-Builds/releases)
  - Managed by the LUG Helper
  - Prebuilt releases from the [TKG](https://github.com/Frogging-Family/wine-tkg-git) build system
  - TKG runners 10.3+ patched to accomodate PTU's easy anti-cheat enforcement


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


## Updating DXVK within a wine prefix
To re-install or update DXVK
  - Navigate to your game prefix directory `~/Games/star-citizen`
  - Run the following in your terminal `./sc-launch.sh shell` then `winetricks --force dxvk`

## NixOS
On NixOS, to set `vm.max_map_count` and `fs.file-max`, add the following to your NixOS config:

```nix
# ... your NixOS Config ...
boot.kernel.sysctl = {
  "vm.max_map_count" = 16777216;
  "fs.file-max" = 524288;
};
```


## RSI Launcher 2.0
- Requires standard Wine 9.4+ or Proton GE 9-13+ runner
  - Recent Wine versions can be easily installed from the Kron4ek runner source in the [LUG Helper](https://github.com/starcitizen-lug/lug-helper)
- In Lutris, right click the game->Configure->Runner options, remove the following DLL override:
  - `powershell.exe: disabled`
- If using standard Wine, winetricks **20250102** or newer is required to install powershell
  1. navigate to your game prefix directory `~/Games/star-citizen`
  2. run the following in your terminal `./sc-launch.sh shell` then `winetricks powershell`
- If using standard Wine, CLI mode must be enabled in Lutris
  - Right click the game -> Configure -> System options -> Toggle on advanced options -> CLI mode
- The 2.0 Launcher may need to be installed manually. See [below](#rsi-launcher-manual-update) for instructions


## RSI Launcher Manual Update
- Download the [latest](https://robertsspaceindustries.com/download) RSI Launcher installer
- Wine:
  - Open a terminal and run `~/Games/star-citizen/sc-launch.sh shell`
  - Then run `wine ~/path/to/your/installer`. Complete the install and **EXIT**
- Lutris: Use the "run EXE inside wine prefix" option and select the RSI Launcher installer. Complete the install and **EXIT**
  ![Screenshot from 2023-05-11 10-33-19](https://github.com/starcitizen-lug/knowledge-base/assets/3657071/d146e9cc-e0a2-4327-acfb-ba5538ddefe4)


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

## Proton
- Install Lutris v0.5.18 or later
- Right click the game, select Configure, and then adjust settings as follows:
- In Runner options, set Wine version to `GE-Proton`
- In Runner options, remove the following DLL override:
  - `powershell.exe: disabled`
- In System options, add the following environment variables:
  - `GAMEID: umu-starcitizen`
  - `PROTONPATH: GE-Proton`
- Other environment variables can be updated/removed if desired by comparing against those set for a new install in our [install json](https://github.com/starcitizen-lug/lug-helper/blob/main/lib/lutris-starcitizen.json)


## Easy Anti-Cheat
> [!note]
> Your wine prefix under Z:\ will be hidden from the file picker, so you will have to manually type or paste the full path.

> [!warning]
> Windows paths use back slashes `\` instead of forward slashes `/`

> [!important]
> EAC will not like symlinks of any directory along your install path. Verify your absolute path if using an immutable distro such as bazzite/ublue

> [!important]
> Check the [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#general-news) for any wine changes

A video of these steps can be found [here](https://www.youtube.com/watch?v=GqyXKT5-kRA).
1. In the RSI Launcher, navigate to `Settings -> Games -> Game Location`
   ![Screenshot From 2024-10-04 23-22-13](https://github.com/user-attachments/assets/01496e30-92cc-4120-ba58-45ec11363f10)
2. Change the RSI Library location to be its absolute path on your linux filesystem from `Z:\`. **No symlinks!**
   - If you installed the game to the default location, change it to the result of this command. Execute the following in a bash shell:
     ```
       echo "Z:$(realpath "$HOME/Games/star-citizen/drive_c/Program Files/Roberts Space Industries")" | sed -e 's/\//\\/g'
     ```
   - If you installed the game elsewhere, `Z:\` is mapped to your filesystem's root. Any path or mountpoint you type in must be referenced from the `Z:\` root.

   ![Screenshot From 2024-10-04 23-20-21](https://github.com/user-attachments/assets/01e31cb8-7cdc-468f-b2a1-658ba173de53)
3. Remove all EAC workarounds
    1. Remove EAC line from `/etc/hosts` file: `127.0.0.1 modules-cdn.eac-prod.on.epicgames.com #Star Citizen EAC workaround`
    2. Lutris: remove the EAC environment variables `EOS_USE_ANTICHEATCLIENTNULL=1` and `SteamGameId=starcitizen`
    3. Non-Lutris: use a text editor to open `sc-launch.sh` and remove `export EOS_USE_ANTICHEATCLIENTNULL=1`
    4. If you have any other EAC workarounds in place, remove them as well.


## AMD FidelityFX Super Resolution (FSR) upscaling
Use the in-game CIG TSR, AMD FSR, or NVIDIA DLSS options, external tools are not recommended

In the Lutris `Runner options` tab, enable `AMD FidelityFX Super Resolution` or set the environment variable `WINE_FULLSCREEN_FSR=1`. Then, in the Star Citizen graphics settings, set the game to fullscreen and your desired resolution and it will be FSR scaled up. We recommend restarting the game after changing its resolution for better performance.


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
