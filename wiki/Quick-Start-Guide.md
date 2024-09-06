## Prerequisites
New to Linux? See our [Recommended Distributions](Tips-and-Tricks#recommended-distros) for a list of the distros most compatible with Star Citizen.

1. Install wine following the instructions for your distro on the [WineHQ website](https://wiki.winehq.org/Category:Distributions). **If your distro provides an up to date version of wine** (ie. Arch), you may install from its repos instead. See the [WineHQ Main Page](https://www.winehq.org/) for current versions.
2. Install Winetricks from your distro's repository. Additional instructions are on the [Winetricks github](https://github.com/Winetricks/winetricks?tab=readme-ov-file#installing).
3. If you want to use Lutris, install [Lutris **v0.5.17**](https://lutris.net/downloads/) or newer and launch it once before installing Star Citizen to trigger its automatic winetricks dependency download. **Note**: We do not recommend running git builds of Lutris.
4. If you want to install without Lutris, install DXVK from your distro's repository.

## Installation Steps
1. Download our [LUG Helper](https://github.com/starcitizen-lug/lug-helper/releases/latest) (distro packages listed [here](https://github.com/starcitizen-lug/lug-helper#installation)).
2. Launch the LUG Helper and run the `Pre-flight Check` to optimize your system settings.
3. In the LUG Helper, select your preferred installation method: `Install Star Citizen with Lutris/Wine`
4. Select an install location on an SSD where you have space for the entire game, approximately 110GB (we do not recommend an HDD).
5. In the RSI Launcher, log in and click install to finish installing the game.  
 **Do not change the default install path in the RSI Launcher settings!**
6. Lutris will use umu/Proton by default. Optionally switch to your System Wine version instead:  
  `Right click the game -> Configure -> Runner options -> Wine version`
7. **Wayland users:** See [required workarounds](https://github.com/starcitizen-lug/knowledge-base/wiki/Troubleshooting#mousecursor-issues-and-view-snapping-in-interaction-mode) to resolve mouse cursor and view snapping issues.
8. Check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for important updates. Especially, Nvidia gpu driver issues and necessary workarounds.
9. Run the launcher and start the game. See you in the 'verse!


> [!tip]
> Questions or Problems? Check our [Troubleshooting Guide](Troubleshooting) or ask for help in one of our [social channels](https://github.com/starcitizen-lug/knowledge-base/wiki#welcome-space-penguins)!

> [!note]
> On first launch, you may see low FPS while shaders are compiled and caches are filled.  
> This can also occur after updating Star Citizen, your graphics driver, Wine, or DXVK.
