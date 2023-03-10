## Prerequisites
New to Linux? See our [Recommended Distributions](Tips-and-Tricks#recommended-distros) for a list of the distros most compatible with Star Citizen.

1. Install wine-staging following the instructions for your distro on the [WineHQ website](https://wiki.winehq.org/Category:Distributions).
2. Install [32 bit drivers](Troubleshooting#-32bit-drivers) for your graphics card.
3. Install [Lutris **v0.5.11**](https://lutris.net/downloads/) or newer and launch it once before installing Star Citizen to trigger its automatic winetricks dependency download. **Note**: We do not recommend running git builds of Lutris.
4. In Lutris' `Preferences->Global options`, `Prefer system libraries` may have to be toggled to either `Off` or `On` depending on your system. Start with `Off`. If you get library version errors during installation, try `On`. After installation is successful, this may be reset and configured on a per-game basis if desired.

## Installation Steps
1. Download our [LUG Helper](https://github.com/starcitizen-lug/lug-helper) (distro packages listed [here](https://github.com/starcitizen-lug/lug-helper#installation))
2. Launch the LUG Helper and run the `Pre-flight Check` to optimize your system settings
3. In the LUG Helper, select `Install Star Citizen` and install the launcher to an SSD (we do not recommend an HDD)
4. When the LUG Helper prompts to you deploy the Easy Anti-Cheat Workaround, select Yes. It can also be deployed from the Main Menu.
5. Run the launcher from Lutris and finish installing the game
6. In the LUG Helper, select `Manage Lutris Runners`, and install the latest runner from GloriousEggroll (or ask us on our [social channels](https://github.com/starcitizen-lug/knowledge-base/wiki#welcome-space-penguins) which runner is currently recommended)
7. In the LUG Helper, select `Manage DXVK Versions`. **AMD:** Install the latest dxvk from Sporif Async. Follow the instructions [on our wiki](Performance-Tuning#dxvk-async) to enable the async environment variable. **Nvidia:** Install the latest dxvk from gnusenpai
8. In Lutris, make sure `Prefer system libraries` is `Off` either globally or just for Star Citizen. If you have no sound in-game or are on a rolling release distro, you may need to set this instead to `On`
9. Check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for important updates. Especially Nvidia gpu driver issues, necessary workarounds, and currently recommended runner/DXVK versions.
10. Run the launcher again and start the game. See you in the 'verse!

## Video Guide
Video guides of the above are available for [AMD](https://www.youtube.com/watch?v=cHGtwIH5ocI) and [Nvidia](https://www.youtube.com/watch?v=QVVPv12RGtk) by Grumpy

## Important Information
> Questions or Problems? Check our [Troubleshooting Guide](Troubleshooting) or ask for help in one of our [social channels](https://github.com/starcitizen-lug/knowledge-base/wiki#welcome-space-penguins)!

> On first launch, the game will stutter with low FPS while shaders are compiled and caches are filled. As you run/fly around and travel to different places, performance will increase.
> This can also occur after updating Star Citizen, your graphics driver, Wine, or DXVK.
