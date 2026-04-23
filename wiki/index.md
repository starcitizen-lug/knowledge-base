---
title: "Home"
nav_order: 1
md_message: "You are viewing raw source files... Go to https://wiki.starcitizen-lug.org/ to use the wiki!"
---

<h1>Star Citizen Linux Users Group Wiki</h1>

<h2>Welcome, Space Penguins!</h2>

This wiki is a collection of information on how to run Star Citizen on Linux. If you're just getting started, head over to our [Quick-Start Guide](Quick-Start-Guide)!

To contribute updates/information, please open an [issue report or pull request](https://github.com/starcitizen-lug/knowledge-base). Thanks!

## Join us!

🐧 <a href="https://robertsspaceindustries.com/orgs/LUG">Star Citizen Org</a>  
🗨 <a href="https://discord.gg/meCFYPj">Discord</a>  

## News

### Game Updates

{: .warning-title }
> (Apr 23, 2026)
>
> Launcher out of space crash when updating/installing Star Citizen.  
> Log may show *"[Pipeline] Phase compute_size timed out after 60000ms, cancelling and skipping."*
> This can be caused by a slow or unreliable network connection
>
> 1. [Locate your Star Citizen LIVE](https://wiki.starcitizen-lug.org/Tips-and-Tricks#where-is-my-wine-prefix-where-is-my-liveptu-directory) directory.
> 2. Create a new empty file in your LIVE directory named `Data.p4k.part`
> 3. If you're installing the game for the first time, also create a new empty file named `Data.p4k`
> 4. Re-launch the game and try the update or verify again.
>
> If the above steps don't work, try rolling back to an older version of the RSI Launcher:
> 1. Download [RSI Launcher v2.12.1](https://install.robertsspaceindustries.com/rel/2/RSI%20Launcher-Setup-2.12.1.exe)
> 2. Open a [Wine maintenance shell](/Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) then run `wine "~/path/to/downloaded/RSI Launcher-Setup-2.12.1.exe"` to install it.
> 3. Type `exit` to close the Maintenance shell, then re-launch the game.
> 4. When the RSI Launcher asks to auto update, cancel the update to remain on v2.12.1 until the issue is fixed.

{: .important-title }
> (Mar 25, 2026)
>
> Launcher error 3221225477
>
> - Use winetricks to install vcrun2022 in your wine prefix
> - Open a [Wine maintenance shell](/Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) then run `winetricks -q vcrun2022` then `exit`


### General News

> none!

### AMD News

> none!


### Nvidia News

> none!
