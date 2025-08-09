---
title: "Troubleshooting"
nav_order: 3
---

## ⚠️ Recent news/issues
- Check our [latest news](/#news) for known temporary issues, workarounds, and runner/dxvk/driver requirements (especially Nvidia users!)

## 🛠️ Troubleshooting Steps

#### First things to try
1. Make sure our [LUG Helper](https://github.com/starcitizen-lug/lug-helper)'s Preflight Check passes all checks.
2. Make sure all prerequisites from the [Quick Start Guide](Quick-Start-Guide) are satisfied on your system.
3. Kill all wine processes and re-launch a fresh instance of the game.
   Navigate to `~/Games/star-citizen` and run the following in your terminal `./sc-launch.sh shell` then `wineserver -k`
5. Look for your issue in the [latest news](/#news)
6. Use the lug helper to get the latest wine runner. Be sure to check the [latest news](/#general-news) for recommendations
7. Try a different wine version. If using wine-staging, try standard wine. Try wine-staging if using standard wine.
8. Look for your issue/error in the categories on this page. Refer to the steps directly below to gather logs.

#### Gathering logs
- Wine log: `~/Games/star-citizen/sc-launch.log`
- Launcher log: `~/Games/star-citizen/drive_c/users/$USER/AppData/Roaming/rsilauncher/logs/log.log`
- Game log: `~/Games/star-citizen/drive_c/Program Files/Roberts Space Industries/StarCitizen/LIVE/Game.log`
- Native Lutris `lutris -d > ~/lutrislog.log`
- Flatpak Lutris `flatpak run net.lutris.Lutris -d > ~/lutrislog.log`


#### Community Help
If this page doesn't help resolve your issue, you may ask for help on our [social channels](/knowledge-base)