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
> (Apr 20, 2026)
>
> Launcher out of space crash when updating/installing Star Citizen.  
> Log may show *"[Pipeline] Phase compute_size timed out after 60000ms, cancelling and skipping."*
>
> - Download [RSI Launcher v2.12.1](https://install.robertsspaceindustries.com/rel/2/RSI%20Launcher-Setup-2.12.1.exe)
> - Open a [Wine maintenance shell](/Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) then run `wine "~/path/to/downloaded/RSI Launcher-Setup-2.12.1.exe"` to install it.
> - Type `exit` to close the Maintenance shell, then relaunche the game.
> - When the RSI Launcher asks to auto update, cancel the update to remain on v2.12.1 until the issue is fixed.

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
