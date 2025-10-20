---
title: "Troubleshooting"
description: "A collection of solutions to errors, crashes, and other common problems running Star Citizen on Linux"
nav_order: 3
---

# 🔧 Troubleshooting

## Recent news/issues

{: .important-title }
Check our [latest news](/#news) for known temporary issues, workarounds, and runner/dxvk/driver requirements (especially Nvidia users!)

## Troubleshooting Steps

### First things to try
1. Make sure our [LUG Helper](/Tips-and-Tricks#how-to-run-the-lug-helper)'s Preflight Check passes all checks.
2. Make sure all prerequisites from the [Quick Start Guide](/Quick-Start-Guide) are satisfied on your system.
3. Make sure you are not trying to install to an NTFS-formatted drive.
4. Be sure you haven't changed the default install path in the RSI Launcher settings. If you wish to install the game elsewhere, put the entire wine prefix there instead.
5. Kill all wine processes and re-launch a fresh instance of the game: Open a [Wine maintenance shell](/Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) then run `wineserver -k`
6. Look for your issue in the [latest news](/#news)
7. Use the lug helper to get the latest wine runner. Be sure to check the [latest news](/#general-news) for recommendations
8. Try a different wine version. If using wine-staging, try standard wine. Try wine-staging if using standard wine.
9. Look for your issue/error in the categories on this page. Refer to the steps directly below to gather logs.


### Gathering logs
- Wine log  
  `~/Games/star-citizen/sc-launch.log`
- Launcher log  
  `~/Games/star-citizen/drive_c/users/$USER/AppData/Roaming/rsilauncher/logs/log.log`
- Game log  
  `~/Games/star-citizen/drive_c/Program Files/Roberts Space Industries/StarCitizen/LIVE/Game.log`
- EAC log  
  `~/Games/star-citizen/drive_c/users/$USER/AppData/Roaming/EasyAntiCheat/(hash)/(hash)/anticheatlauncher.log`


### View game files
- Default location  
  `~/Games/star-citizen/drive_c/Program Files/Roberts Space Industries/StarCitizen`
- Use the [LUG Helper](/Tips-and-Tricks#how-to-run-the-lug-helper) to find your game files  
  1. Select `Maintenance and Troubleshooting` > `Display Helper and Star Citizen Directories`  
  2. Click on the link to your game directory

### Search for your issue in the Troubleshooting pages

{: .tip }
> Use the search box at the top of this wiki to search for your error, crash, or problem.
> 
> You may also look through the relevant sections of the Table of Contents below for your problem.

### Community Help
If you can't find a solution to your issue in the Troubleshooting subpages, you may ask for help on our [social channels](/#join-us).
