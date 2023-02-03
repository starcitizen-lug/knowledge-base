# Welcome, Space Penguins!

This wiki is a collection of information on how to run Star Citizen on Linux, as well as our tips and tricks!

🐧 Join us! https://robertsspaceindustries.com/orgs/LUG  

🗨 Discord: https://discord.gg/meCFYPj  
😎 Matrix space: https://matrix.to/#/#SCLUG:matrix.org  

## Contents
* [Quick-Start Guide](https://github.com/starcitizen-lug/information-howtos/wiki/Quick-Start-Guide)
* [Manual Installation](https://github.com/starcitizen-lug/information-howtos/wiki/Manual-Installation)
* [LUG Wine Builds](https://github.com/starcitizen-lug/information-howtos/wiki/Wine-Builds-for-Star-Citizen)
* [Performance Tuning](https://github.com/starcitizen-lug/information-howtos/wiki/Performance-Tuning)
* [Tips and Tricks](https://github.com/starcitizen-lug/information-howtos/wiki/Tips-and-Tricks)
* [Common Issues and Solutions](https://github.com/starcitizen-lug/information-howtos/wiki/Common-Issues-and-Solutions)

## News

**Game Updates**

> (Jan 27, 2023) **RSI Launcher v1.6.2**  
>
> Special configuration is needed in Lutris or you will receive a java error. See [CIG's announcement in Spectrum](https://robertsspaceindustries.com/spectrum/community/SC/forum/1/thread/upcoming-launcher-update-for-linux-users/5693728  )
>
> **Solution 1:**
> - **After the launcher updates,** all Penguins must configure the following:
>   - `Right click the game->Configure->Game options` add `--no-sandbox` to the Arguments
>   - In `System options`, make sure Advanced options is on then enable `CLI mode`
>
> **Solution 2:**
> - **If this does not fix the problem**, revert the above changes and install the latest GloriousEggroll runner, available in our Helper

> (Jan 27, 2023) **Fresh installs fail to create needed directories**
> - This has been resolved in the latest version of our [Helper](https://github.com/starcitizen-lug/lug-helper/releases). For other install methods, manually run the following command to create the necessary directory structure for both the LIVE and PTU environments. Adjust the wine prefix path if installing to a non-default location:  
> ```
> mkdir -p "/home/$USER/Games/star-citizen/drive_c/Program Files/Roberts Space Industries/StarCitizen/"{LIVE,PTU}
> ```

> (Dec 23, 2022) **3.18 PTU**  
> - The 3.18 update may cause mouse issues for some people using Wayland. Using Gamescope with the game is a workaround, and can be easily enabled through Lutris or manually.

**General News**

> (Jan 22, 2023) **Game install hangs**
> - Some Penguins are reporting hangs during installation. In Lutris, setting `Prefer system libraries` to `Off` globally before installation fixes the problem. After installation, this can be reset and configured only for Star Citizen if desired.

> (Oct 14, 2022) **No sound in game**
> - Penguins on rolling release distributions (ie. Arch, Manjaro) are reporting issues with no sound in-game. The solution is to set `Prefer System Libraries` in Lutris to `ON`.

**Nvidia News**

> (Jan 27, 2023) **Required DXVK version**
> - DXVK 2.1 may resolve issues Penguins had with previous versions of DXVK and may perform better without async.
> - For DXVK 2.0 and prior, Penguins with RTX cards should use [gnusenpai DXVK v1.10.1 or later](https://github.com/gnusenpai/dxvk/releases) to fix the `corrupted size vs. prev_size` error/crash. Can be installed manually or from the LUG helper.

> (Nov 17, 2022) **DXVK 2.0**
> - DXVK 2.0 changes the way shaders are handled on some Nvidia cards and may provide better performance than async (see the [release notes](https://github.com/doitsujin/dxvk/releases/tag/v2.0)). If you have worse performance on 2.0, remove the the `DXVK_ASYNC=1` environment variable.
> - DXVK 2.0 requires Nvidia driver **v510.47.03** or later, but **v520.56.06** or later is recommended.

> (Oct 20, 2022) **Graphics driver out of date**
> - You may see a popup that your graphics driver is out of date. This is a warning that can be ignored. To remove this warning, disable `DXVK-NVAPI/DLSS` in your Lutris runner options.

**Easy Anti-Cheat**

> (Feb 12, 2022) **Easy Anti-Cheat is live.**
> - CIG is aware of the problem but there is still no ETA. There are currently no consequences that we are aware of for using the workaround, but CIG has suggested that eventually people will be kicked for tripping EAC. To apply the workaround, use the [LUG Helper](https://github.com/starcitizen-lug/lug-helper).

test
test
