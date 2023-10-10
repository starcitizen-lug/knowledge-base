## ⚠ Recent news/issues
- Check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for known temporary issues, workarounds, and runner/dxvk/driver requirements (especially Nvidia users!)

## Troubleshooting Steps

1. Make sure our [LUG Helper](https://github.com/starcitizen-lug/lug-helper)'s Preflight Check passes all checks
2. Make sure all prerequisites from the [Quick Start Guide](Quick-Start-Guide) are satisfied on your system
3. Check Lutris logs by clicking the arrow beside the play button:  
  ![Screenshot from 2023-04-15 14-09-40](https://user-images.githubusercontent.com/3657071/232246219-8d713782-2d22-474c-a350-921e4af430af.png)
4. Run Lutris in debug mode to see more verbose logging. Native: `lutris -d` Flatpak: `flatpak run net.lutris.Lutris -d`
5. Look for your issue in the [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) and the list of common issues below
6. Ask for help on our [social channels](https://github.com/starcitizen-lug/knowledge-base/wiki#welcome-space-penguins)


### Contents
💾 [Install & Update Problems](#-install--update-problems)  
💥 [Crashes](#-crashes)  
🧊 [Freezes](#-freezes)  
🤪 [Unexpected Behavior (sometimes also crashes)](#-unexpected-behavior-sometimes-also-crashes)  
💚 [Nvidia](#-nvidia)  
❤️ [AMD](#-amd)  
🕹️ [Controller Issues](#-controller-issues)  
🦦 [Lutris Issues](#-lutris-issues)  
👾 [32bit Drivers](#-32bit-drivers)  
❔ [Other Issues](#-other-issues)  

***



## 💾 Install & Update Problems

#### Launcher hangs during installation
- In Lutris, try setting `Prefer system libraries` to `Off` globally before installation. After installation, this can be reset and configured only for Star Citizen if desired.

#### Install button does nothing
- ⚠️ Launch Lutris in debug mode (`lutris -d`) and look for a `KeyError: 'contentstatsid'` error.
- If the error is present, check your Lutris version. This is fixed in v0.5.11. https://lutris.net/downloads


#### Error: *utf-8 codec can't decode byte 0x_ in position ___: invalid continuation byte*
- Re-check your EAC workaround. Our [Helper](https://github.com/starcitizen-lug/lug-helper) can check it for you, or see the [manual instructions](Tips-and-Tricks#easy-anti-cheat-workaround) on our wiki.


#### Warning: Downloading [exe file] failed
- If you get download failed errors during installation for components such as `arial32.exe`, try toggling `Prefer system libraries` in Lutris to `On`.


#### Library version errors during installation
- If using a rolling release or bleeding edge distro, try toggling `Prefer system libraries` in Lutris to `On`.


#### RSI Launcher doesn't auto-update
- GE runners seem to prevent auto-updates. Temporarily switching to standard wine may allow the update to install
- Alternatively, [download](https://robertsspaceindustries.com/download) the latest launcher and install it by selecting `Run EXE inside Wine prefix` in Lutris:  
  ![Screenshot from 2023-05-11 10-33-19](https://github.com/starcitizen-lug/knowledge-base/assets/3657071/d146e9cc-e0a2-4327-acfb-ba5538ddefe4)



#### Installing Star Citizen on an NTFS-formatted drive
- See: https://github.com/ValveSoftware/Proton/wiki/Using-a-NTFS-disk-with-Linux-and-Windows

***




## 💥 Crashes

#### RSI Launcher v1.6.2+ JavaScript error
- For more information, see [CIG's announcement in Spectrum](https://robertsspaceindustries.com/spectrum/community/SC/forum/1/thread/upcoming-launcher-update-for-linux-users/5693728)
- Solution 1:
   - `Right click the game->Configure->Game options` add `--no-sandbox` to the Arguments
   - In `System options`, make sure Advanced options is on then enable `CLI mode`
- Solution 2:
  - If this does not fix the problem, revert the above changes and install the latest GloriousEggroll runner, available in our [Helper](https://github.com/starcitizen-lug/lug-helper)


#### Code 3 crash with error: *Star Citizen process exited abnormally (code: 3) : Command failed*
- You are likely missing 32bit drivers. See [32bit Drivers](#-32bit-drivers) below for more information
- Additionally, explicitly set the Vulkan ICD loader in Lutris to either `Nvidia Proprietary` or `AMD RADV Open Source`
  - Right click the game -> Configure -> System options -> Vulkan ICD loader
- If you are using the Flatpak Lutris, you may need to resync it with your system after installing the 32bit drivers. Run: `flatpak update`


#### Game immediately crashes after clicking 'Launch'
- Start by checking the Wine output and/or "game.log" file

- Possible cause 1: DXVK
  - Make sure DXVK is enabled in Lutris' Runner options.
  - Some people report changing their DXVK version fixes this. Try using our [Helper](https://github.com/starcitizen-lug/lug-helper) to download an async DXVK.
  - Nvidia users, check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for gpu driver issues, necessary workarounds, and currently recommended runner/DXVK versions.
  - DXVK installation instructions are available on our wiki [here](Performance-Tuning#dxvk-async).

- Possible cause 2: Incorrect Vulkan ICD Loader
  - If you have Intel integrated graphics and see `VK_ICD_FILENAMES="/usr/share/vulkan/icd.d/intel_hasvk_icd.x86_64.json` in your log, then change the Vulkan ICD Loader in Lutris to use your discrete GPU:
  ![image](https://user-images.githubusercontent.com/3657071/221420185-c1f1e346-b67f-4cd9-ba14-748668a266ed.png)

- Possible cause 3: Phantom joystick
  - Many keyboards and mice can also have a "joystick" part in Linux, which Wine can detect. Unfortunately, Wine may be confused about it, as they are not real joysticks. In this case, the game could crash. Try running the Wine joystick control panel "wine control" (in Lutris: right click -> Joystick configuration) and disable your keyboard and/or mice.
  - This will not affect how your keyboard and mice work in the game.


#### Game crashes after clicking 'Verify'
- Make sure Star Citizen is installed on drive "C:\" Check the "Library Folder" option in the launcher settings:  
![Star Citizen launcher](https://media.discordapp.net/attachments/608349808956276737/927652866389340310/Screenshot_from_2022-01-03_14-56-37.png)
- Additionally, make sure the wine prefix is not installed on an NTFS formatted partition.


#### Game crashes with "STATUS_CRYENGINE_FATAL_ERROR" in game.log
- Some penguins have had success changing the Windows compatibility from Win10 to Win8.1 in the Wine configuration. Select Star Citizen in Lutris, then click the Wine button at the bottom and select `Wine configuration`:  
![](https://matrix-client.matrix.org/_matrix/media/r0/download/matrix.org/zKGOXxMOsktqYKqevqeSvYSw)  
- In the Wine configuration, under the `Applications` tab, change `Windows version` to `Windows 8.1`

#### Game crashes with "create_view: Assertion `!((UINT_PTR)base & page_mask)' failed."
- Make sure you have set your vm.max_map_count as described in the installation section.

#### Game crashes with " 00adntdll:FILE_GetNtStatus Converting errno 12 to STATUS_UNSUCCESSFUL "
- Make sure you have set your vm.max_map_count as described in the installation section.


#### Game crashes with "Failed to initialize dependencies" error
- Make sure the `SDL_VIDEODRIVER` environment variable is **NOT** set globally to `wayland` on your system.


#### After playing for a while, game/lutris/wine crash, no errors
  - If there are no errors in your game logs, check your system logs. It may be an Out Of Memory situation. Create a larger [swap file](Performance-Tuning#swap).


#### Game crashes when going to Lorville / ArcCorp or crashes often when launching
- Make sure you followed the guide to install Wine's dependencies and set your vm.max_map_count as described in the installation section.

***




## 🧊 Freezes

#### Game hangs at splash screen or black/transparent window after clicking 'Launch'
- Make sure DXVK is enabled in Lutris' Runner options.
- Try changing to a different DXVK version in the Lutris settings.  Alternate DXVKs can be quickly installed using our [LUG Helper](https://github.com/starcitizen-lug/lug-helper).
- Nvidia users, check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for gpu driver issues, necessary workarounds, and currently recommended runner/DXVK versions.
- DXVK installation instructions are available on our wiki [here](Performance-Tuning#dxvk-async).


#### Launcher freezes within a few seconds of opening
- Try using a different runner. Ask on Spectrum or in our social channels which runner is currently recommended.
- Alternatively, you can try changing "Prefer system libraries" to ON, although this may have other side effects.
  - Right click the game -> Configure -> System options -> Prefer system libraries


#### Launch Game stuck at "launching..."
- ⚠️ Launch Lutris in debug mode (`lutris -d`) and look for a `KeyError: 'contentstatsid'` error.
- If the error is present, check your Lutris version. This is fixed in v0.5.11. https://lutris.net/downloads


#### Launcher hangs / stops responding / crashes with an "ASAR" error
- Some people report the launcher hanging in combination with the Lutris runtime. If you are on Lutris, try toggling "Disable Lutris runtime" under "System options" of the Lutris game options.
- If you do need to disable the Lutris runtime, the Lutris guys would like to have a log file to debug the issue. You can run lutris -d from the terminal after enabling Wine debugging as per this image:  
![Enable Wine debugging](https://robertsspaceindustries.com/imager/Xeh-bNe8P9_WE60v7iLpmeXXLzI=/fit-in/400x400/https://cdn.discordapp.com/attachments/540589766811451392/558481590687236096/Peek_2019-03-22_05-43.gif)
- And send a log to @beniwtv on Spectrum or send it to Lutris developers in the Lutris Discord.

***




## 🤪 Unexpected Behavior (sometimes also crashes)

#### Mouse/Cursor issues and view snapping in interaction mode
- The 3.18 update caused mouse and view snapping issues for most Penguins using Wayland. We recommend installing Gamescope as a workaround or using Xorg.
- **Note for Nvidia users:** Gamescope may not work on your hardware. See this [known issue report](https://github.com/ValveSoftware/gamescope/issues/526).
- A possible fix to get Gamescope working on Nvidia: `Right click the game->Configure->System options->Game execution->Environment variables` then select `__GL_THREADED_OPTIMIZATIONS` and click `Delete` located beneath the `Environment variables` table.
- After installing Gamescope, enable it in Lutris: `Right click the game->Configure->System options->Gamescope->Enable Gamescope`. Then, set `Output Resolution` to your monitor's native resolution, ie `1920x1080`.
- If you're using a version of gamescope newer than **3.11.51**, an additional Gamescope setting is required. Set `Relative Mouse Mode` to on
- Other Gamescope settings that may be required depending on your system: `Window Mode` set to `Fullscreen` if it doesn't launch fullscreen, `-g` in `Custom Settings` to grab keyboard
- Depending on your system, `Prefer System Libraries` may need to be enabled or disabled in Lutris
- If this doesn't work, you will need to switch to Xorg instead of Wayland.


#### Empty launcher
- Log out log back in, or reset the launcher by pressing Ctrl+Shift+Alt+R


#### Visual glitches or semi-transparent lines, poor performance, possibly random crashes
- DXVK is likely disabled in Lutris's Runner options. Make sure it is enabled.
- Your game shader cache may need to be cleared. Our [Helper](https://github.com/starcitizen-lug/lug-helper) can quickly clear your game shaders.
![](https://media.discordapp.net/attachments/608349808956276737/1070664567425871960/SC_Lines.jpg)


#### No sound in game
- Depending on your distribution, you may need to set `Prefer System Libraries` in Lutris to `ON`.
- If you have sound in the launcher but not in the game, launch the game and go to your audio settings, then enable "Play sound while game is in background".


#### DirectX error message
- Error may read "Star Citizen requires DirectX feature level of 11.1 as a minimum which is not supported at present on this machine"  
  ![image](https://user-images.githubusercontent.com/3657071/224719841-ba1e831b-4ace-4f14-b423-3e49528154c6.png)
- Check that the `Vulkan ICD loader` is not set to an integrated gpu (ie, Intel)
   - Right click the game -> Configure -> System options -> Vulkan ICD loader
- Also make sure your GPU drivers (Mesa/nvidia) are up to date and DXVK is enabled/updated.


#### Failed to initialize dependencies error
- Make sure the `SDL_VIDEODRIVER` environment variable is **NOT** set globally to `wayland` on your system. This causes incompatibilities with many games. If it is, simply unset it.


#### Black or flickering window, possible crash with errors 15006 or 30007
- Check for larger resolutions and scaling settings.  See CIG's [support article](https://support.robertsspaceindustries.com/hc/en-us/articles/360000081887-Guide-to-Graphic-Issues#large-res)


#### Black/transparent window after clicking 'Launch'
- Make sure DXVK is enabled in Lutris' Runner options.
- Try changing to a different DXVK version in the Lutris settings.  Alternate DXVKs can be quickly installed using our [LUG Helper](https://github.com/starcitizen-lug/lug-helper).
- Nvidia users, check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for gpu driver issues, necessary workarounds, and currently recommended runner/DXVK versions.
- DXVK installation instructions are available on our wiki [here](Performance-Tuning#dxvk-async).


#### Launcher white screen / error DCompositionCreateDevice
- In Lutris, configure Star Citizen (right-click->Configure->Game options) and add `"--use-gl=osmesa"` to the Arguments field.
- If launching manually: `wine "RSI Launcher.exe" "--use-gl=osmesa"`

***




## 💚 Nvidia

#### Current known issues
- See the Nvidia section of our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for the ways in which Nvidia is being special today.

#### Popup saying your Nvidia graphics driver is out of date
- Ignore or Disable DXVK NVAPI in Lutris.
  - Right click the game -> Configure -> Runner options -> Enable DXVK-NVAPI/DLSS (set to off)

#### Severe frame drops
- Some Penguins are seeing VRAM exhaustion problems on nvidia cards. It appears to be driver related and does not seem to affect AMD cards.
- The 530 series of drivers appears to make this problem worse. Switching to 525 may help, see [this thread](https://forums.developer.nvidia.com/t/vram-allocation-issues/239678/20).
- Other workarounds that some Penguins have had some success with:
   - Create a new `dxvk.conf` file and add `d3d11.cachedDynamicResources = "a"` to it, then either export `DXVK_CONFIG_FILE=path/to/dxvk.conf` or, if using Lutris, add `DXVK_CONFIG_FILE` as a new environment variable in the game's settings and set it to the file path.
   - If you still have issues or are running applications like OBS, you may also have to limit the vram the game sees to free up some vram for other applications:
     `dxgi.maxDeviceMemory = 6144`


***




## ♥ AMD

#### Everything just works
- Congrats on choosing AMD

***



## 🕹 Controller Issues

- See our sticks, throttles, and pedals [Troubleshooting Page](Sticks,-Throttles,-&-Pedals#troubleshooting)

***



## 🦦 Lutris Issues

#### In Lutris, right clicking on Star Citizen and selecting "Configure" does not bring up the configuration
- Completely close Lutris with `kill lutris`, delete everything inside the Lutris cache directory `~/.cache/lutris`, and relaunch Lutris.

***


## 👾 32bit Drivers

#### Arch-based Distributions (Arch, EndeavourOS, Manjarno, etc)
1. Enable the [multilib repo](https://wiki.archlinux.org/title/Official_repositories#Enabling_multilib)
2. Install 32bit drivers
- AMD
  ```
  sudo pacman -S --needed lib32-mesa vulkan-radeon lib32-vulkan-radeon vulkan-icd-loader lib32-vulkan-icd-loader
  ```
- Nvidia
  ```
  sudo pacman -S --needed nvidia-dkms nvidia-utils lib32-nvidia-utils nvidia-settings vulkan-icd-loader lib32-vulkan-icd-loader
  ```

#### Ubuntu & Friends (Ubuntu, Mint, PopOS, etc)
- AMD
  ```
  sudo dpkg --add-architecture i386 && sudo apt update && sudo apt upgrade && sudo apt install libgl1-mesa-dri:i386 mesa-vulkan-drivers mesa-vulkan-drivers:i386
  ```
- Nvidia
  ```
  sudo dpkg --add-architecture i386 && sudo apt update && sudo apt install -y nvidia-driver-525 libvulkan1 libvulkan1:i386
  ```

#### Fedora & Derivatives (Fedora, Nobara, etc)
- TBA

#### openSUSE Tumbleweed
- AMD
  ```
  sudo zypper in kernel-firmware-amdgpu libdrm_amdgpu1 libdrm_amdgpu1-32bit libdrm_radeon1 libdrm_radeon1-32bit libvulkan_radeon libvulkan_radeon-32bit libvulkan1 libvulkan1-32bit
  ```
- Nvidia
   1. Follow the instructions here: https://en.opensuse.org/SDB:NVIDIA_drivers
   2. Install 32bit drivers by appending the `-32bit` suffix to the driver package names
   3. Install vulkan libraries:
      ```
      sudo zypper in libvulkan1 libvulkan1-32bit
      ```

#### Gentoo 💪
- We defer to your expertise



## ❔ Other Issues

#### Workarounds For In-Game Bugs and Annoyances
- https://robertsspaceindustries.com/spectrum/community/LUG/forum/149/thread/known-workarounds-for-game-bugs-and-annoyances

⚠️ Join the org to access Spectrum links: https://robertsspaceindustries.com/orgs/LUG
