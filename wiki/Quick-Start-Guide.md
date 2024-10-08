## Prerequisites
New to Linux? See our [Recommended Distributions](Tips-and-Tricks#recommended-distros) for a list of the distros most compatible with Star Citizen.

1. Install wine following the [instructions for your distro](https://gitlab.winehq.org/wine/wine/-/wikis/Download). See the [WineHQ Main Page](https://www.winehq.org/) for current versions. **If your distro provides an up to date version of wine** (ie. Arch), you may install from its repositories instead.
2. Install [32 bit drivers](Troubleshooting#-32bit-drivers) for your graphics card.
3. Install [Lutris **v0.5.11**](https://lutris.net/downloads/) or newer and launch it once before installing Star Citizen to trigger its automatic winetricks dependency download. **Note**: We do not recommend running git builds of Lutris. If using an immutable distro (ie. Bazzite, Nix, Silverblue), we recommend flatpak Lutris.
4. In Lutris' `Preferences->Global options`, `Prefer system libraries` may have to be toggled to either `On` or `Off` depending on your system. For most distros, this should be `On`. After installation is successful, this may be reset or configured on a per-game basis as needed.

## Installation Steps
1. Download our [LUG Helper](https://github.com/starcitizen-lug/lug-helper/releases/latest) (distro packages listed [here](https://github.com/starcitizen-lug/lug-helper#installation)).
2. Launch the LUG Helper and run the `Pre-flight Check` to optimize your system settings.
3. In the LUG Helper, select `Install Star Citizen` and install the launcher to an SSD where you have space for the entire game, approximately 110GB (we do not recommend an HDD or NTFS).
4. Run the RSI launcher from Lutris and finish installing the game; do not change the default install path in the RSI Launcher settings.
5. In the LUG Helper, select `Manage Lutris Runners`, and install the latest runner from GloriousEggroll (or ask us on our [social channels](https://github.com/starcitizen-lug/knowledge-base/wiki#welcome-space-penguins) which runner is currently recommended).
6. In the LUG Helper, select `Manage DXVK Versions`. Install the latest standard dxvk.
7. **Wayland users:** See [required workarounds](https://github.com/starcitizen-lug/knowledge-base/wiki/Troubleshooting#mousecursor-issues-and-view-snapping-in-interaction-mode) to **resolve mouse cursor and view snapping issues when holding F key**
8. Check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for important updates. Especially, Nvidia gpu driver issues, necessary workarounds, and currently recommended runner/DXVK versions.
9. Run the launcher again and start the game. See you in the 'verse!

## Important Information
> Questions or Problems? Check our [Troubleshooting Guide](Troubleshooting) or ask for help in one of our [social channels](https://github.com/starcitizen-lug/knowledge-base/wiki#welcome-space-penguins)!

> On first launch, the game will stutter with low FPS while shaders are compiled and caches are filled. As you run/fly around and travel to different places, performance will increase.
> This can also occur after updating Star Citizen, your graphics driver, Wine, or DXVK.
