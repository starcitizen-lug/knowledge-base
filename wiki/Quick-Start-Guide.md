## Prerequisites
- New to Linux? See our [Recommended Distributions](Tips-and-Tricks#recommended-distros) for a list of the distros most compatible with Star Citizen.
- Star Citizen requires an SSD with enough space for the entire game, approximately 110GiB (we do not recommend an HDD).

## Installation
### Native WINE
1. Install wine following the [instructions for your distro](https://gitlab.winehq.org/wine/wine/-/wikis/Download). See the [WineHQ Main Page](https://www.winehq.org/) for current versions. **If your distro provides an up to date version of wine** (ie. Arch), you may install from its repositories instead.
2. Download our [LUG Helper](https://github.com/starcitizen-lug/lug-helper/releases/latest) (Select the `.tar.gz`. Distro packages are listed [here](https://github.com/starcitizen-lug/lug-helper#installation)).
3. Launch the LUG Helper and run the Preflight Check to fix any issues it finds before proceeding!
4. Once pre-flight passes select `Install Star Citizen with Wine`.
5. Select an install location on an SSD where you have space for the entire game.
6. Run the RSI Launcher, log in, and click install to finish installing the game.
7. Launch the game. See you in the 'verse!

### Lutris
1. Install [Lutris **v0.5.17**](https://lutris.net/downloads/) or newer and launch it once before installing Star Citizen to trigger its automatic winetricks dependency download. **Note**: We do not recommend running git builds of Lutris. If using an immutable distro (ie. Bazzite, Nix, Silverblue), we recommend flatpak Lutris.
2. Download our [LUG Helper](https://github.com/starcitizen-lug/lug-helper/releases/latest) (Select the `.tar.gz`. Distro packages are listed [here](https://github.com/starcitizen-lug/lug-helper#installation)).
3. Launch the LUG Helper and run the Preflight Check to fix any issues it finds before proceeding!
4. Once pre-flight passes select `Install Star Citizen with Lutris`.
5. Select an install location on an SSD where you have space for the entire game.
6. If using Lutris v0.5.17, you must add `GAMEID=umu-starcitizen PROTONPATH=GE-Proton` into `Right click the game->Configure->System options->Command prefix`. You must also install `gamemode` using your system's package manager.

> [!warning]
> You will need to remove the command prefix when Lutris v0.5.18 is released!

7. Run the RSI Launcher, log in, and click install to finish installing the game.
8. Launch the game. See you in the 'verse!

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
10. Run the RSI Launcher, log in, and click install to finish installing the game.
11. Launch the game. See you in the 'verse!

## Additional Notes
> [!important]
> Star Citizen currently requires a workaround to get EAC working. Instructions available [here](https://github.com/starcitizen-lug/knowledge-base/wiki/Tips-and-Tricks#easy-anti-cheat) and apply to all install methods.

> [!tip]
> Questions or Problems? Check our [Troubleshooting Guide](Troubleshooting) or ask for help in one of our [social channels](https://github.com/starcitizen-lug/knowledge-base/wiki#welcome-space-penguins)!

> [!tip]
> Wayland users: See [required workarounds](Troubleshooting#mousecursor-warp-issues-and-view-snapping-in-interaction-mode) to resolve mouse cursor and view snapping issues.

> [!tip]
> Check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for important updates. Especially, Nvidia gpu driver issues and necessary workarounds.

> [!note]
> On first launch, you may see low FPS while shaders are compiled and caches are filled.  
> This can also occur after updating Star Citizen, your graphics driver, Wine, or DXVK.
