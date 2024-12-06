## Prerequisites
> [!tip]
> New to Linux? See our [Recommended Distributions](Tips-and-Tricks#recommended-distros) for a list of the distros most compatible with Star Citizen.

1. Install Wine **v9.4** or newer following the [instructions for your distro](https://gitlab.winehq.org/wine/wine/-/wikis/Download). See the [WineHQ Main Page](https://www.winehq.org/) for current versions. If your distribution provides an up to date version of wine (ie. Arch), you may install from its repositories instead.
2. Install any version of winetricks from your distribution's repositories. Links, if needed, are on the winetricks [github](https://github.com/Winetricks/winetricks#installing). This pulls in some needed dependencies.
3. Lutris is optional. If you want to use it, install [Lutris **v0.5.18**](https://lutris.net/downloads/) or newer and launch it once before installing Star Citizen to trigger its automatic winetricks dependency download. **Note**: We do not recommend running git builds of Lutris. If using an immutable distro (ie. Bazzite, Nix, Silverblue), we recommend flatpak Lutris.

## Installation Steps
1. Download our [LUG Helper](https://github.com/starcitizen-lug/lug-helper/releases/latest) (Select the `.tar.gz`. Distro packages are listed [here](https://github.com/starcitizen-lug/lug-helper#installation)).
2. Launch the LUG Helper and select your preferred installation method. We recommend the non-Lutris `Install Star Citizen with Wine`.
3. Allow the Preflight Check to fix any issues it finds before proceeding!
4. Select an install location on a linux-formatted SSD where you have space for the entire game, approximately 110GB (we do not recommend an HDD or NTFS).
5. If using Lutris, change the runner to `UMU-Latest` in the game's runner configuration tab.
6. Run the RSI Launcher, log in, and click install to finish installing the game.
7. Launch the game. See you in the 'verse!

> [!important]
> - Check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for necessary workarounds, Nvidia gpu driver problems, and other important issues.
> - Wayland users: See [required workarounds](Troubleshooting#mousecursor-warp-issues-and-view-snapping-in-interaction-mode) to resolve mouse cursor and view snapping issues.  

> [!tip]
> Questions or Problems? Check our [Troubleshooting Guide](Troubleshooting) or ask for help in one of our [social channels](https://github.com/starcitizen-lug/knowledge-base/wiki#welcome-space-penguins)!

> [!note]
> On first launch, you may see low FPS while shaders are compiled and caches are filled.  
> This can also occur after updating Star Citizen, your graphics driver, Wine, or DXVK.
