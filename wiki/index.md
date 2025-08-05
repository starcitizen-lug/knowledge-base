---
title: "Home"
nav_order: 1
---

<h1>Welcome, Space Penguins!</h1>

This wiki is a collection of information on how to run Star Citizen on Linux, as well as our tips and tricks!
We welcome contributions. Feel free to fork this repo and submit a PR.

🐧 Join us! <a href="https://robertsspaceindustries.com/orgs/LUG">https://robertsspaceindustries.com/orgs/LUG</a>  
🗨 Discord: <a href="https://discord.gg/meCFYPj">https://discord.gg/meCFYPj</a>  
😎 Matrix space: <a href="https://matrix.to/#/#SCLUG:matrix.org">https://matrix.to/#/#SCLUG:matrix.org</a>  

## News

### Game Updates

{: .important-title }
> (July 11, 2025)
>
> Easy Anticheat enforcement has been enabled on LIVE
>
> - We're ready! Follow the instructions [here](Tips-and-Tricks#easy-anti-cheat) to fix your existing install. New installs via the Helper handle it automagically.


### General News

{: .note-title }
> (Jul 10, 2024)
>
> Star Citizen requires DirectX feature level of 11.1 as a minimum
>
> - Wine staging + Latest DXVK can cause issues for nvidia users
> - Switch to a non-staging wine **OR** downgrade DXVK following [these instructions](Troubleshooting#directx-error-message)


{: .note-title }
> (Nov 30, 2024)
>
> Joysticks not detected on Wine 9.22 and newer
>
> - Wine 9.22+ has enabled HIDRAW by default for VKB and Virpil devices.
> - If your joystick/throttle is no longer being detected by the game, follow [our instructions](Sticks,-Throttles,-&-Pedals#some-of-your-joysticks-disappear--arent-recognized-in-the-game) to enable hidraw access.

### AMD News

> none


### Nvidia News

{: .caution-title }
> (Oct 9, 2023)
>
> Crash when taking shield damage in-game
>
> - There is a shield rendering bug that causes the game to crash. It seems to affect 1000 series cards.
> - There is currently no known workaround other than switching cards. We recommend AMD.
