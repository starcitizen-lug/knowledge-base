# Welcome, Space Penguins!

This wiki is a collection of information on how to run Star Citizen on Linux, as well as our tips and tricks!

🐧 Join us! https://robertsspaceindustries.com/orgs/LUG  

🗨 Discord: https://discord.gg/meCFYPj  
😎 Matrix space: https://matrix.to/#/#SCLUG:matrix.org  

## Contents
* [Quick-Start Guide](Quick-Start-Guide)
* [Manual Installation](Manual-Installation)
* [Troubleshooting](Troubleshooting)
* [Performance Tuning](Performance-Tuning)
* [Tips and Tricks](Tips-and-Tricks)
* [Sticks, Throttles, & Pedals](Sticks,-Throttles,-&-Pedals)

## News

#### Game Updates
> (Apr 11, 2024) **2.0 Launcher (Beta) error 2000 "error_os_requirements_text"**
> - Launcher 2.0 beta fails to download the game
>   - To fix: switch to a wine 9.4+ or proton GE 9-5+ runner
> - Launcher 2.0 beta is unable to verify files, use install button instead

> (Jan 27, 2023) **Fresh installs fail to create needed directories**
> - This has been resolved in the latest version of our [Helper](https://github.com/starcitizen-lug/lug-helper/releases/latest) for new installs.
> - For existing or manual installs, run the following command to create the necessary directory structure for LIVE, PTU, and other environments. Adjust the wine prefix path if installing to a non-default location:  
> ```
> mkdir -p "/home/$USER/Games/star-citizen/drive_c/Program Files/Roberts Space Industries/StarCitizen/"{LIVE,PTU,HOTFIX,EPTU,TECH-PREVIEW}
> ```


#### General News
> (May 4, 2024) **Game Crash on launch from main menu**
> - Linux kernel 6.8.9 can result in a crash when launching from main menu, may be accompanied by a popup including text "Assertion failed!"
>   - To fix: revert to kernel 6.8.8, update to 6.9+, or enable ReBar if your hardware supports it

> (Jan 15, 2024) **Installer Error Code 256**
> - Lutris version [5.15 had a critical bug](https://github.com/lutris/lutris/releases/tag/v0.5.16)  preventing successful installations of games
>   - To fix: update to latest Lutris 5.17

> (Nov 11, 2023) **Failed to Initialize Dependencies**
> - If you are on a rolling release distro and using Gamescope, you may receive this error due to a bug in Gamescope v3.12.7. See [this Github issue](https://github.com/ValveSoftware/gamescope/issues/984) for more info.
>   - To fix: Install the git release of Gamescope or downgrade to 3.12.5 until the fix is released to stable.

> (Oct 24, 2023) **Installer Error Code 256**
> - Set "Prefer system libraries" to enabled in global lutris options
> - Inspect install log for failed winetricks downloads or sha256 mismatch and note the URL of the files being downloaded and its destination in winetricks' cache
> - Download each file manually to its destination in winetricks' cache
> - Use winetricks to ensure that the prefix is set to Win10 mode
> - Proceed with lug-helper installer


#### AMD News
> (Apr 29, 2024) **Vulkan Beta**
> - Bright flickering lights at edges of ingame RTT display panels
>   - To fix: Add environment variable `radv_zero_vram=true`
> - Game may present a black screen
>   - To fix: Add environment variable `dual_color_blend_by_location=true`
>   - Alternatively copy `/usr/share/drirc.d/00-radv-defaults.conf` to `~/.drirc`
>   - Add the following to `~/.drirc`:
> ```
> <application name="Star Citizen" executable="StarCitizen.exe" >
>      <option name="dual_color_blend_by_location" value="true" />
> </application>
> ```


#### Nvidia News
> (Apr 29, 2024) **Vulkan Beta**
> - Game fails to launch with vulkan renderer enabled
>   - Use latest wine-GE 8-26+
>   - Add environment variable `WINE_HIDE_NVIDIA_GPU=1`

> (Oct 9, 2023) **Crash when taking shield damage in-game**
> - There is a shield rendering bug that causes the game to crash. It seems to affect 1000 series cards.
> - There is currently no known workaround other than switching cards. We recommend AMD.


#### Easy Anti-Cheat
> (Feb 12, 2022) **Easy Anti-Cheat is live.**
> - CIG is aware of the problem but there is still no ETA. There are currently no consequences that we are aware of for using the workaround, but CIG has suggested that eventually people will be kicked for tripping EAC. The workaround is automatically configured for new installs through Lutris.
