---
title: "💥 Crashes"
description: "Known issues that can cause crashes in Star Citizen on Linux + troubleshooting steps to resolve them"
parent: "Troubleshooting"
nav_order: 2
md_message: "You are viewing raw source files... Go to https://wiki.starcitizen-lug.org/ to use the wiki!"
---

# 💥 Crashes


## Code 3 crash with error: *Star Citizen process exited abnormally (code: 3) : Command failed*
- EAC bootstrapper failed to start up
- Explicitly set the DXVK device name
  - identify device name using command `vulkaninfo --summary | grep deviceName`
  - set device name with environment variable `DXVK_FILTER_DEVICE_NAME=yourdevicenamehere`
- If using a flatpak launcher, you may need to resync it with your system. Run: `flatpak update`


## Game immediately crashes after clicking 'Launch'
- Start by checking the Wine output and/or "game.log" file. See [initial troubleshooting steps and gathering logs](/Troubleshooting/#troubleshooting-steps).

- See [latest news](/#news) for information on recent stability issues.

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


## Game launcher fails to start

- Possible cause: Outdated glibc
  - Log message may include `could not load ntdll.so ... version 'GLIB-C_x.xx not found'`
  - Update to the latest release of a [non-LTS distro](/Tips-and-Tricks#recommended-distros)


## Game crashes after clicking 'Verify'
- Make sure Star Citizen is installed on drive "C:\" Check the "Library Folder" option in the launcher settings:
![Star Citizen launcher](https://github.com/user-attachments/assets/0ac1ed3a-4c3c-43b9-b93a-a4865e63f784)
- Additionally, make sure the wine prefix is not installed on an NTFS formatted partition.oh keep in mind might be interesting to see what the model produces


## Game crashes after loading into the PU
- Make sure you have set [your vm.max_map_count](/Alternative-Installations#prerequisites) and passed all LUG Helper preflight checks


## Crash when using Vulkan with error: Assertion failed! or vkCreateSwapchainKHR
- [Edit the launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) and add the following environment variable:  
    `export MESA_VK_WSI_PRESENT_MODE=mailbox`
- You may need to revert to DX11 by creating a [USER.cfg](/Tips-and-Tricks#usercfg) file.


## After playing for a while, crash with no errors
  - If there are no errors in your [game logs](/Troubleshooting/#gathering-logs), check your system logs. It may be an Out Of Memory situation. Create a larger [swap file](/Performance-Tuning#zram--swap).


## Launcher freezes within a few seconds of opening
- Try using a different [wine runner](/Tips-and-Tricks#recommended-runners)
