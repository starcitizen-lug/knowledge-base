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

> [!important]
> (July 11, 2025) **Easy Anticheat Enforcement has been Enabled on LIVE**
> 
> - We're ready! Follow the instructions [here](Tips-and-Tricks#easy-anti-cheat) to fix your existing install. New installs via the Helper handle it automagically.


### General News

> [!note]
> (Jul 10, 2024) **Star Citizen requires DirectX feature level of 11.1 as a minimum**
> - Wine staging + Latest DXVK can cause issues for nvidia users
> - Switch to a non-staging wine **OR** downgrade DXVK following [these instructions](Troubleshooting#directx-error-message)


> [!note]
> (Nov 30, 2024) **Joysticks not detected on Wine 9.22 and newer**
> - Wine 9.22+ has enabled HIDRAW by default for VKB and Virpil devices.
> - If your joystick/throttle is no longer being detected by the game, follow [our instructions](Sticks,-Throttles,-&-Pedals#some-of-your-joysticks-disappear--arent-recognized-in-the-game) to enable hidraw access.

### AMD News

> none


### Nvidia News

> [!caution]
> (Oct 9, 2023) **Crash when taking shield damage in-game**
> - There is a shield rendering bug that causes the game to crash. It seems to affect 1000 series cards.
> - There is currently no known workaround other than switching cards. We recommend AMD.
