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

## NixOS
On NixOS, to set `vm.max_map_count` and `fs.file-max`, add the following to your NixOS config:

```nix
# ... your NixOS Config ...
boot.kernel.sysctl = {
  "vm.max_map_count" = 16777216;
  "fs.file-max" = 524288;
};
```


## AMD FidelityFX Super Resolution (FSR) upscaling
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


## Easy Anti-Cheat
1. In the RSI Launcher, navigate to `Settings -> Games -> Game Location`
   ![image](https://github.com/user-attachments/assets/95312ca4-78eb-4c0d-8be3-a1d246ee8a8e)
2. Update the RSI Library location to be its absolute path on your linux filesystem from `Z:\`  
   - If you installed the game to the default location, change it to the following. Don't forget to adjust your username:
   - `Z:\home\{user}\Games\star-citizen\drive_c\Program Files\Roberts Space Industries`
   - If you installed the game elsewhere, `Z:\` is mapped to your filesystem's root. Any path or mountpoint you type in must be referenced from the `Z:\` root
3. In Lutris, delete the EAC environment variable `EOS_USE_ANTICHEATCLIENTNULL`  
   `Right click the game -> Configure -> System options -> Environment variables`
> [!important]
> Your wine prefix under Z:\ will be hidden from the file picker, so you will have to manually type or paste the full path.


## Lutris Pre-launch and Post-exit Scripts
Below are sample pre-launch and post-exit scripts that incorporate the mouse acceleration workarounds described above.
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


## Updating DXVK within a wine prefix
1. Update winetricks:  
   `sudo winetricks --self-update`
3. Re-install dxvk (change wine prefix to match your install location):  
   `WINEPREFIX=$HOME/Games/star-citizen winetricks dxvk`
