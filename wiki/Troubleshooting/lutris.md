---
title: "🦦 Lutris Issues"
parent: "Troubleshooting"
nav_order: 5
---

# 🦦 Lutris Issues

## Lutris General troubleshooting steps
- In Lutris, try setting `Prefer system libraries` to `On` globally before installation. After installation, this can be reset and configured only for Star Citizen if desired.
- Kill all wine processes and re-launch a fresh instance of the game. Select the game, click the arrow beside the wine button, choose `Open Bash terminal` and run `wineserver -k` and then restart.

{: .important }
> Our current recommended install method is to use the [LUG Helper](/Quick-Start-Guide#installation-steps) to install the game without Lutris. If this page does not help resolve your issue, we recommend reinstalling the game using the LUG Helper. Tip: Back up and restore your data.p4k file to avoid re-downloading the entire game.

## In Lutris, right clicking on Star Citizen and selecting "Configure" does not bring up the configuration
- Completely close Lutris with `kill lutris`, delete everything inside the Lutris cache directory `~/.cache/lutris`, and relaunch Lutris.


## Launcher hangs / stops responding / crashes with an "ASAR" error
- Some people report the launcher hanging in combination with the Lutris runtime. If you are on Lutris, try toggling "Disable Lutris runtime" under "System options" of the Lutris game options.


## RSI Launcher v1.6.2+ JavaScript error
- The LUG Helper's [wine installation](/Quick-Start-Guide#installation-steps) method is recommended and avoids this error
- In the game's Lutris `System options`, make sure Advanced options is toggled on then in the `text-based games` section enable `CLI mode`
- Alternatively, see our updated [lutris setup instructions](/Alternative-Installations#lutris) for current runner/settings recommendations


## Library version errors during installation
- If using a rolling release or bleeding edge distro, try toggling `Prefer system libraries` in Lutris to `On`.


## Installer Error Code 256 / Downloading [exe file] failed (ie arial32.exe)
- Try setting `Prefer system libraries` to `On` in global lutris options.
- Inspect install log for failed winetricks downloads or sha256 mismatch, note the URL of the files being downloaded and its destination in winetricks' cache.
- Download each file manually to its destination in winetricks' cache.
- Use winetricks to ensure that the prefix is set to Win10 mode.


## Lutris error: *Command exited with code 512*
- We suspect this is a Lutris bug and fixes seem inconsistent.
- Try going to Lutris Preferences -> Sources, and toggle either `Lutris` or `Local` and then toggle it back again.
- If you have an old install, try importing that into Lutris.


## Lutris error: *"Runtime Error('No path can be generated for DXVK because no version information is available.')"*
- If you've just installed Lutris, be sure to launch it once, separately from the Star Citizen install process, to fully populate its runtime and caches.


## RSI Launcher white screen / error DCompositionCreateDevice
- In Lutris, configure Star Citizen (right-click->Configure->Game options) and add `"--use-gl=osmesa"` to the Arguments field.
- If launching manually: `wine "RSI Launcher.exe" "--use-gl=osmesa"`


## RSI Launcher fails to launch from lutris with CLI mode enabled
- Error message may be similar to `/usr/bin/gnome-terminal.real: symbol lookup error: /lib/x86_64-linux-gnu/libatk-bridge-2.0.so.0: undefined symbol: atk_component_scroll_to`
- Disable the lutris runtime in lutris global preferences to work around this error


## No sound in game
- Depending on your distribution, you may need to set `Prefer System Libraries` in Lutris to `ON`.
- If you have sound in the launcher but not in the game, launch the game and go to your audio settings, then enable "Play sound while game is in background".
