---
title: "💥 Crashes"
parent: "Troubleshooting"
nav_order: 2
---

# 💥 Crashes

## Error Code 210 and #1 Crash
- Standard Wine versions >10.1 made changes that break Easy Anti-Cheat
- Use the Helper to switch to a [recommended](/Tips-and-Tricks#recommended-runners) wine runner


## Code 3 crash with error: *Star Citizen process exited abnormally (code: 3) : Command failed*
- EAC bootstrapper failed to start up
- You may be missing 32bit drivers. See [32bit Drivers](32bit-drivers) below for more information
- Additionally, explicitly set the DXVK device name
  - identify device name using command `vulkaninfo --summary | grep deviceName`
  - set device name with environment variable `DXVK_FILTER_DEVICE_NAME=yourdevicenamehere`
- If using a flatpak launcher, you may need to resync it with your system. Run: `flatpak update`


## Game immediately crashes after clicking 'Launch'
- Start by checking the Wine output and/or "game.log" file

- See [latest news](/#general-news) for information on recent stability issues

- Possible cause: DXVK
  - Make sure DXVK is installed and enabled
  - Nvidia users, check our [latest news](/#news) and Nvidia [section](nvidia) for gpu driver issues, necessary workarounds, and currently recommended runner/DXVK versions.

- Possible cause: Incorrect Vulkan device
  - If you have Intel integrated graphics and see  
    `VK_ICD_FILENAMES="/usr/share/vulkan/icd.d/intel_hasvk_icd.x86_64.json` in your log, then change the Vulkan device to use your discrete GPU:
    - identify device name using command `vulkaninfo --summary | grep deviceName`
    - set device name with environment variable `DXVK_FILTER_DEVICE_NAME=yourdevicenamehere`

- Possible cause: GPU drivers not working properly
  - If, in your "game.log", you see only `llvmpipe` listed as the working video adapter, your gpu drivers may not be functioning properly.

- Possible cause: Out of date flatpak libraries/packages
  - If you are using flatpak and have not run `flatpak update` recently, this should be done regularly to keep everything up to date.

- Possible cause: Phantom joystick
  - Many keyboards and mice can also have a "joystick" part in Linux, which Wine can detect. Unfortunately, Wine may be confused about it, as they are not real joysticks. In this case, the game could crash. Use the LUG Helper's maintenance menu to run the wine control panel and disable your keyboard and/or mice.


## Game crashes after clicking 'Verify'
- Make sure Star Citizen is installed on drive "C:\" Check the "Library Folder" option in the launcher settings:
![Star Citizen launcher](https://github.com/user-attachments/assets/0ac1ed3a-4c3c-43b9-b93a-a4865e63f784)
- Additionally, make sure the wine prefix is not installed on an NTFS formatted partition.oh keep in mind might be interesting to see what the model produces


## Game crashes after loading into the PU
- Make sure you have set [your vm.max_map_count](/Alternative-Installations#prerequisites) and passed all LUG Helper preflight checks


## Crash or black screen while using Vulkan beta renderer
- Possible error similar to: `Fatal Error: Acquire Next Image Failed` or `Main thread considered to be deadlocked`
- Check the [latest news](/#news) for recommendations for your graphics card
- Go back to DX11 by using the Delete Shaders option in the RSI Launcher > Settings > Games > {LIVE,PTU} > Delete  Local Settings > Shaders folder


## Failed to decompress file/corrupted block detected error
- Some Penguins have had this error when using BTRFS. We suspect a regression of some kind.
- Easiest: Just ignore the error and continue playing. It doesn't crash until you click the button.
- Or fix it: Disable CoW on the game's StarCitizen dir
  1. Navigate to the Game folder `star-citizen/drive_c/Program Files/Roberts Space Industries`
  2. Use a terminal to run the command ```chattr +C ./StarCitizen```, then redownload or copy in a fresh data.p4k.
- Less easy Fix: Disable CoW only on the data.p4k file. This can only be done on an empty file.
- Alternatively, try mounting with the `compress` option instead of `compress-force`.
- If that doesn't work, switching to ext4 is an option.


## After playing for a while, crash with no errors
  - If there are no errors in your [game logs](/Troubleshooting/#gathering-logs), check your system logs. It may be an Out Of Memory situation. Create a larger [swap file](/Performance-Tuning#zram--swap).


## Game hangs at splash screen or black/transparent window after clicking 'Launch'
- Make sure DXVK is installed. Use the [LUG Helper](https://github.com/starcitizen-lug/lug-helper) to install it
- Nvidia users, check our [latest news](/#news) for gpu driver issues, necessary workarounds, and currently recommended runner/DXVK versions.


## Launcher freezes within a few seconds of opening
- Try using a different wine runner
