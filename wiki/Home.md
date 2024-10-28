# Welcome, Space Penguins!

This wiki is a collection of information on how to run Star Citizen on Linux, as well as our tips and tricks!  
We welcome contributions. Feel free to fork this repo and submit a PR.  

🐧 Join us! https://robertsspaceindustries.com/orgs/LUG  

🗨 Discord: https://discord.gg/meCFYPj  
😎 Matrix space: https://matrix.to/#/#SCLUG:matrix.org  

## Contents
* [Quick-Start Guide](Quick-Start-Guide)
* [Alternative Installations](Alternative-Installations)
* [Troubleshooting](Troubleshooting)
* [Performance Tuning](Performance-Tuning)
* [Tips and Tricks](Tips-and-Tricks)
* [Sticks, Throttles, & Pedals](Sticks,-Throttles,-&-Pedals)
* [Head Tracking](Head-Tracking)

## News

### Game Updates
> [!note]
> (Oct 28, 2024) **You're trying to run the game on an unsupported Windows OS**
> - Just click OK.

> [!warning]
> (Oct 25, 2024) **Vulkan crashes in 3.24.1/3.24.2**
> - Black screen, crash
> - Possible error similar to: `Fatal Error: Acquire Next Image Failed`
> - If you experience this, we recommend remaining on DX11 for now

> [!warning]
> (Oct 25, 2024) **Launcher installation hangs at Updating Game Content**
> - The 2.0 Launcher seems to sometimes hang during this phase of the install process
> - Completely quit the launcher, ensuring no lingering wine processes remain, then verify files

> [!important]
> (Oct 4, 2024) **Easy Anticheat Enforcement**
> 
> - CIG has enabled EAC enforcement on the PTU. We have an experimental fix that also works on LIVE and it needs testing.
> - Please follow [our migration instructions](Tips-and-Tricks#easy-anti-cheat) and report back on our Discord's #Development channel.

> [!important]
> (Aug 23, 2024) **Vulkan Beta: Limited performance with KDE on Wayland**
> - Vulkan renderer on kde wayland may result in your [gpu utilisation being limited to less than 75%](https://bugs.kde.org/show_bug.cgi?id=492051), causing low framerates
>   - To fix: either use Gamescope, switch to another desktop, or run KDE's x11 session


### General News
> [!warning]
> (Sept 21, 2024) **Wine-staging causes launcher to hang when downloading base pack, may cause game crashes**
> - We recommend using standard Wine instead of Wine-staging
> - Recent Wine versions can be easily installed from the Kron4ek runner source in the [LUG Helper](https://github.com/starcitizen-lug/lug-helper)


### AMD News


### Nvidia News
> [!warning]
> (Oct 9, 2024) **Black screen**
> - Wine 9.18 introduced a regression for Nvidia in how it handles Vulkan
> - Update to Wine 9.20

> [!warning]
> (Apr 29, 2024) **Vulkan Beta: Game fails to launch**
> - There is an [issue with LibCUDA](https://github.com/jp7677/dxvk-nvapi/issues/174#issuecomment-2227462795) that prevents vulkan and DLSS from working on linux.
> - If using Wine-GE, add the environment variable `WINE_HIDE_NVIDIA_GPU=1` to enable vulkan
> - If using Wine or Wine-GE, see [instructions](https://github.com/starcitizen-lug/knowledge-base/wiki/Troubleshooting#dlssdeep-learning-super-sampling--vulkan) to patch libcuda to enable both vulkan and DLSS
> - [Proton](https://github.com/starcitizen-lug/knowledge-base/wiki/Tips-and-Tricks#proton) enables both vulkan and DLSS

> [!caution]
> (Oct 9, 2023) **Crash when taking shield damage in-game**
> - There is a shield rendering bug that causes the game to crash. It seems to affect 1000 series cards.
> - There is currently no known workaround other than switching cards. We recommend AMD.
