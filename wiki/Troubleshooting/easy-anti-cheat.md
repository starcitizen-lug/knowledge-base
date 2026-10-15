---
title: "🤡 Easy Anti-Cheat"
description: "Known Easy Anti-Cheat compatibility issues and helpful troubleshooting steps to resolve them"
parent: "Troubleshooting"
nav_order: 5
md_message: "You are viewing raw source files... Go to https://wiki.starcitizen-lug.org/ to use the wiki!"
---

# 🤡 Easy Anti-Cheat


{: .important-title }
>
> Check the [latest news](/#news) for any changes

1. Use RSI Launcher 2.5.1 or newer
2. Ensure there are no **symlinks** or **special characters** in the path to your Wine prefix
3. Ensure you have **not** changed the default install location in the RSI Launcher  
   ```
   C:\Program Files\Roberts Space Industries
   ```
5. Use the latest [LUG Helper](/Tips-and-Tricks#how-to-add-a-wine-runner) to switch to the latest LUG-Wine runner

## Error code after launching persistent universe
- Possible error codes `70003`, `70004`
- [game.log](/Troubleshooting#gathering-logs) message may contain `Remote Disconnect - Authentication timed out (1/3)` or `HeartbeatTimeout`
- Try changing server region
- Inspect your [EAC log](/Troubleshooting/#gathering-logs) for details. It may be launching with the null client if it can't reach the EAC servers.
- [Locate your game files](/Troubleshooting#view-game-files) then delete the EAC directories and use the RSI Launcher to Verify Files  
  ```
  ~/Games/star-citizen/drive_c/Program Files/Roberts Space Industries/StarCitizen/LIVE/EasyAntiCheat
  ```  
  ```
  ~/Games/star-citizen/drive_c/users/{yourusernamehere}/AppData/Roaming/EasyAntiCheat
  ```  
- Use a [Wine maintenance shell](/Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) to run `wineserver -k` to kill any lingering wine processes in your prefix. Reboot if necessary.
- Check that your DNS can resolve the EAC domains:
  ```
  dig modules-cdn.eac-prod.on.epicgames.com
  dig download-alt.easyanticheat.net
  ```
- Ensure that you have **not** disabled development syscalls (e.g. ptrace)
- Check that IPv6 has not been disabled on your system
- Contribute to this [issue council report](https://issue-council.robertsspaceindustries.com/projects/STAR-CITIZEN/issues/STARC-177971) if none of the above steps work


## Error after pressing Launch Game
- Possible error codes `210` and `#1`
- Vanilla Wine versions >10.1 made changes that break Easy Anti-Cheat
- Use the [LUG Helper](/Tips-and-Tricks#how-to-add-a-wine-runner) to switch to a [recommended](/Tips-and-Tricks#recommended-runners) wine runner
- Ensure you have **not** changed the default install location in the RSI Launcher  
  ```
  C:\Program Files\Roberts Space Industries
  ```


## Failed to load the embedded resources
- Possible game error code `60099`
- This can occur of your system is set to certain languages'
- To fix, use the LUG-Helper to [edit your launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) and add the following environment variable:
    - `export LC_ALL=en_US.utf8`
