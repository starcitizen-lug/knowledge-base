---
title: "🤡 Easy Anti-Cheat"
description: "Known Easy Anti-Cheat issues + troubleshooting steps to resolve them"
parent: "Troubleshooting"
nav_order: 4
---

# 🤡 Easy Anti-Cheat


{: .important-title }
>
> Check the [latest news](/#general-news) for any changes

1. Use RSI Launcher 2.5.1 or newer
2. Ensure there are no symlinks or special characters in the path to your Wine prefix
3. Use the latest [LUG Helper](/Tips-and-Tricks#how-to-add-a-wine-runner) to switch to a LUG-Wine runner
4. [Update your launch script](/Tips-and-Tricks#how-to-update-the-launch-script)
5. Remove any EAC workarounds by [editing your launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) or your game launcher settings, check for each one to see if it exists
    - Remove Environment variable `EOS_USE_ANTICHEATCLIENTNULL=1`
    - Remove Hosts entry in file named `/etc/hosts` with the value
      ```
      127.0.0.1 modules-cdn.eac-prod.on.epicgames.com #Star Citizen EAC workaround
      ```
    - In the RSI Launcher, navigate to `Settings -> Games -> LIVE -> Game Location`. If you previously used the Z:\ path workaround, put it back to the default C:\ path  
       ![Game path in launcher](https://github.com/user-attachments/assets/0ac1ed3a-4c3c-43b9-b93a-a4865e63f784){: style="display: block;max-height: 250px;" }  

## Error code after launching persistent universe
- Possible error codes 70003, 70004
- [game.log](/Troubleshooting#gathering-logs) message may contain `Remote Disconnect - Authentication timed out (1/3)`
- [Locate your game files](/Troubleshooting#view-game-files) then delete the EAC directories and use the RSI Launcher to Verify Files  
  ```
  drive_c/Program Files/Roberts Space Industries/StarCitizen/LIVE/EasyAntiCheat
  ```  
  ```
  drive_c/users/{yourusernamehere}/AppData/Roaming/EasyAntiCheat
  ```


  ## Error after pressing Launch Game
- Possible error codes 210 and #1
- Vanilla Wine versions >10.1 made changes that break Easy Anti-Cheat
- Use the Helper to switch to a [recommended](/Tips-and-Tricks#recommended-runners) wine runner
