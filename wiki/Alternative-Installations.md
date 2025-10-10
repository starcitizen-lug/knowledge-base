---
title: "Alternative Installations"
description: "Instructions for installing Star Citizen on Linux using third party launchers and other alternative options to our recommended install via the LUG Helper"
nav_order: 3
---
# Alternative Installations

## Prerequisites

{: .tip-title }
> New to Linux?
>
> See our [Recommended Distributions](Tips-and-Tricks#recommended-distros) for a list of the distros most compatible with Star Citizen.

{: .tip }
> Our [LUG Helper](https://github.com/starcitizen-lug/lug-helper) tool can perform these steps for you automatically! See our [Quick Start Guide](Quick-Start-Guide) for instructions.

1. Install Wine **v9.4** or newer following the [instructions for your distro](https://gitlab.winehq.org/wine/wine/-/wikis/Download). See the [WineHQ Main Page](https://www.winehq.org/) for current versions. If your distro provides an up to date version of wine (ie. Arch), you may install from its repos instead.
2. Install winetricks 20240105-next or newer. Instructions are on the Winetricks [Github](https://github.com/Winetricks/winetricks/#installing)
4. Set `vm.max_map_count` on your system to at least `16777216`
5. Set the Hard open file descriptors limit on your system to at least `524288`

**To check and set vm.max_map_count temporarily**
```
sysctl vm.max_map_count => To check the value
sudo sysctl -w vm.max_map_count=16777216 => To set it temporarily
```

**To set vm.max_map_count permanently**

_Distributions using sysctl.d: Manjaro / Antergos / Arch / Arch-based (probably) / Ubuntu (and probably derivatives) / Fedora_

* Create a new drop-in config file: `/etc/sysctl.d/99-starcitizen-max_map_count.conf`
* Add the following line to the file: `vm.max_map_count = 16777216`
* To reload it, run `sudo sysctl --system`


_Distributions that use sysctl.conf_

* Append the same line to `/etc/sysctl.conf`
* To reload it, run `sudo sysctl --system`

**To set your system's hard open file descriptors limit**

_Distributions using systemd: Manjaro / Antergos / Arch / Arch-based (probably) / Ubuntu (and probably derivatives) / Fedora_

* Create a new drop-in config file: `/etc/systemd/systemd.conf.d/99-starcitizen-filelimit.conf`
* Add the following line to the file: `DefaultLimitNOFILE=524288`
* To reload it, run `sudo systemctl daemon-reexec`

_Distributions that use /etc/security/limits.conf_

* Add the following line to /etc/security/limits.conf: `* hard nofile 524288`


## Wine Installation

{: .tip }
> Our [LUG Helper](https://github.com/starcitizen-lug/lug-helper) tool can perform these steps for you automatically! See our [Quick Start Guide](Quick-Start-Guide) for instructions.

1. Install and configure the necessary prerequisites
2. Create and configure your wine prefix:
   ```
   WINEPREFIX=$HOME/Games/star-citizen winetricks -q arial tahoma dxvk powershell win11
   ```
3. Download and run the RSI installer:
   ```
   WINEPREFIX=$HOME/Games/star-citizen WINEDLLOVERRIDES="dxwebsetup.exe,dotNetFx45_Full_setup.exe=d" wine "~/Downloads/RSI Launcher-Setup-2.3.1.exe" /S
   ```
4. An example launch script is provided on our [LUG Helper's Repo](https://github.com/starcitizen-lug/lug-helper/blob/main/lib/sc-launch.sh)


## Proton Installation

1. Install Open Wine Components [umu-launcher](https://github.com/Open-Wine-Components/umu-launcher/releases/latest)
2. Download and run the RSI Launcher installer:
   ```
   GAMEID="umu-starcitizen" WINEDLLOVERRIDES="dxwebsetup.exe,dotNetFx45_Full_setup.exe=d" umu-run "~/Downloads/RSI Launcher-Setup-2.3.1.exe" /S
   ```
4. Run the RSI Launcher:
   ```
   GAMEID="umu-starcitizen" PROTONPATH="GE-Latest" umu-run "~/Games/umu/umu-starcitizen/drive_c/Program Files/Roberts Space Industries/RSI Launcher/RSI Launcher.exe"
   ```

## Flatpak Installation
Flatpak repository or [latest release](https://github.com/mactan-sc/rsilauncher/releases/latest)  
For documentation and issues refer to [https://github.com/mactan-sc/rsilauncher](https://github.com/mactan-sc/rsilauncher)  
1.  Add the repo
```
flatpak remote-add --user --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak remote-add --user --if-not-exists RSILauncher https://mactan-sc.github.io/rsilauncher/RSILauncher.flatpakrepo
```
2.  install the rsi launcher flatpak
```  
flatpak install -y --user --noninteractive RSILauncher io.github.mactan_sc.RSILauncher
```
3.  run the rsi launcher flatpak
```
flatpak run io.github.mactan_sc.RSILauncher
```
4. Refer to [documentation](https://github.com/mactan-sc/rsilauncher) for configuration tips including setting the game location

## NixOS Installation

The [nix-citizen](https://github.com/LovingMelody/nix-citizen) flake is the recommended install method. Please see the repository for instructions. This flake provides a module to configure your NixOS config for running Star Citizen. Packages for both standard wine and proton methods are available. To try without adding anything to your configuration, you can use the following command:

```bash
nix run github:LovingMelody/nix-citizen#star-citizen
```

If you prefer not to use nix-citizen, the [Flatpak method](#flatpak-installation) is recommended.

If not using the module included in nix-citizen, set `vm.max_map_count` and `fs.file-max` by adding the following to your NixOS config:

```nix
# ... your NixOS Config ...
boot.kernel.sysctl = {
  "vm.max_map_count" = 16777216;
  "fs.file-max" = 524288;
};
```

## Steam Deck Installation
The Steam Deck is resource limited and Star Citizen performance will be poor. Some Penguins have been able to run the game with the following configuration:
- We recommend a 32gb+ [swap file](/Performance-Tuning#zram--swap) for the Steam Deck. Create it under `/home` instead of `/` to protect it from being wiped out by SteamOS updates.
- Configure the max allocation of ram to vram
- Install Star Citizen using the [flatpak method](#flatpak-installation) or a flatpak [third party launcher](#third-party-launchers)


## Third Party Launchers

{: .warning }
> We cannot guarantee that these third party launchers will work with Star Citizen or perform well. Our community may not be able to provide support for these installations if something isn't working right.
>
> The recommended installation method is to follow our [Quick Start Guide](Quick-Start-Guide).

{: .important }
>
> If using flatpak apps, ensure the install location is whitelisted using Flatseal or similar methods.
>
> The Star Citizen launcher does not support temp paths via xdg-portals.

### Lutris
1. Set the default wine runner to GE-Proton in global preferences
2. Install Star Citizen from [Lutris](https://lutris.net/games/star-citizen/)
3. Run the RSI Launcher, log in, and click install to finish installing the game

### Heroic Games Launcher
1. Download latest [Star Citizen installer](https://robertsspaceindustries.com/download).
2. Install [Heroic Games Launcher](https://heroicgameslauncher.com/downloads).
3. Launch Heroic, browse to `Wine Manager>Proton-GE` and install `Proton-GE-Latest`.
4. Return to the Library page, and click Add Game.
5. Set Title to `Star Citizen`.
6. Click `Show Wine Settings` and ensure Wine Version is set to `Proton-GE-Latest`.
7. Click `Run Installer First` and select the Star Citizen install file.
8. Once install is complete, set `Select Executable` to the `RSI Launcher.exe` and click Finish.
9. Open the game settings in Heroic, change to Advanced tab and under Environment Variables add `GAMEID=umu-starcitizen`.
10. Run the RSI Launcher, log in, and click install to finish installing the game

### Bottles
1. Create a new gaming bottle
2. Change the wine runner to GE-Proton or "system wine" 10.0
3. Use the "Install Programs..." Star Citizen option
4. Run Star citizen, log in, and click install to finish installing the game

### Faugus Launcher
1. Download latest [Star Citizen installer](https://robertsspaceindustries.com/download)
2. Press the "New" button
3. Set title to "Star Citizen"
4. Set the Path value to the RSI Installer file you downloaded
5. Set the prefix to your preferred location e.g. `~/Games/star-citizen`
6. Set the Protonfix value to `umu-starcitizen` on the Tools tab
7. Press the "Play" button to run the installer, then exit
8. Right click the game and set the "path" value to the RSI Launcher executable in the wine prefix
9. Press the "Play" button to run the RSI Launcher, log in, and click install tto finish installing the game

### Steam

{: .highlight }
> We do not recommend installing Star Citizen within Steam. While it can be done, it creates several issues that we feel are not worth the effort to try to work around. For example, it limits configurability options and does not invoke needed protonfixes by default.
> 
> We believe you will have a much better experience following our [Quick Start Guide](Quick-Start-Guide). If you want to use Steam's proton, you may use umu-launcher by following the [Proton Installation](#proton-installation) instructions above.
