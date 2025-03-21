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
> (March 1, 2025) **30K errors**
> - 30K the first time you try to join a server. The solution is to return to the menu and try again

> [!note]
> (Oct 28, 2024) **You're trying to run the game on an unsupported Windows OS**
> - Just click OK.

> [!warning]
> (Oct 25, 2024) **Vulkan crashes**
> - Black screen, crash
> - Possible error similar to: `Fatal Error: Acquire Next Image Failed` or `Main thread considered to be deadlocked`
> - If you experience this, [we recommend using DX11 for now](https://github.com/starcitizen-lug/knowledge-base/wiki/Troubleshooting#crash-or-black-screen-while-using-vulkan-beta-renderer)

> [!important]
> (Oct 4, 2024) **Easy Anticheat Enforcement**
> 
> - CIG has enabled EAC enforcement on the PTU. We have an experimental fix that also works on LIVE and it needs testing.
> - Please follow [our migration instructions](Tips-and-Tricks#easy-anti-cheat) and report back on our Discord's #tech-support channel.


### General News

> [!warning]
> (Feb 7, 2025) **Game fails to launch with Wine 10.1 and newer**
> - Game [fails to launch](https://bugs.winehq.org/show_bug.cgi?id=57830) on Wine 10.1+ — Use the LUG Helper's "manage runners" options to pick a different runner
>   - Any Wine 10.0
>   - RawFox 10.3-stg or Kron4ek 10.3 staging-tkg or newer

> [!note]
> (Nov 30, 2024) **Joysticks not detected on Wine 9.22 and newer**
> 
> - Wine 9.22+ has enabled HIDRAW by default for VKB and Virpil devices.
> - If your joystick/throttle is no longer being detected by the game, follow [our instructions](Sticks,-Throttles,-&-Pedals#some-of-your-joysticks-disappear--arent-recognized-in-the-game) to enable hidraw access.

### AMD News


### Nvidia News
> [!warning]
> (Apr 29, 2024) **Vulkan Beta: Game fails to launch**
> - There is an [issue with LibCUDA](https://github.com/jp7677/dxvk-nvapi/issues/174#issuecomment-2227462795) that prevents vulkan and DLSS from working on linux.

> [!caution]
> (Oct 9, 2023) **Crash when taking shield damage in-game**
> - There is a shield rendering bug that causes the game to crash. It seems to affect 1000 series cards.
> - There is currently no known workaround other than switching cards. We recommend AMD.
