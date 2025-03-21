## ⚠ Recent news/issues
- Check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for known temporary issues, workarounds, and runner/dxvk/driver requirements (especially Nvidia users!)

## Troubleshooting Steps

#### First things to try
1. Make sure our [LUG Helper](https://github.com/starcitizen-lug/lug-helper)'s Preflight Check passes all checks.
2. Make sure all prerequisites from the [Quick Start Guide](Quick-Start-Guide) are satisfied on your system.
3. Kill all wine processes and re-launch a fresh instance of the game:
   - If not using Lutris, then navigate to `~/Games/star-citizen` and run the following in your terminal `./sc-launch.sh shell` then `wineserver -k`
   - If using Lutris, select the game, click the arrow beside the wine button, choose `Open Bash terminal` and run `wineserver -k`
     ![Screenshot From 2024-09-30 12-03-57](https://github.com/user-attachments/assets/dd131abb-3adb-4876-a6e6-2c0226884a71)
4. Look for your issue in the [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news)
5. Use the lug helper to get the latest wine runner. Be sure to check the [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#general-news) for recommendations
6. Try a different wine version. If using wine-staging, try standard wine. Try wine-staging if using standard wine.
7. Look for your issue/error in the categories on this page. Refer to the steps directly below to gather logs.

#### Gathering logs
- If not using Lutris, inspect wine's output in `sc-launch.log` in your `~Games/star-citizen` directory
- If using Lutris, check logs by clicking the arrow beside the play button:  
  ![Screenshot from 2023-04-15 14-09-40](https://user-images.githubusercontent.com/3657071/232246219-8d713782-2d22-474c-a350-921e4af430af.png)
  - Run Lutris in debug mode to see more verbose logging  :
   Native: `lutris -d` Flatpak: `flatpak run net.lutris.Lutris -d`
  - If CLI mode is turned on, there will be additional useful output in your terminal window.


#### Community Help
If this page doesn't help resolve your issue, you may ask for help on our [social channels](https://github.com/starcitizen-lug/knowledge-base/wiki#welcome-space-penguins)


## Contents
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

#### General troubleshooting steps
- Refer to [First things to try](#first-things-to-try) above.
- In Lutris, try setting `Prefer system libraries` to `On` globally before installation. After installation, this can be reset and configured only for Star Citizen if desired.
- Make sure you are not trying to install to an NTFS-formatted drive.
- Be sure you haven't changed the default install path in the RSI Launcher settings. If you wish to install the game elsewhere, put the entire wine prefix there instead.


#### Launcher installation hangs at Updating Game Content
- The Launcher sometimes hangs during this phase of the install process
- Completely quit the launcher, ensuring no lingering wine processes remain, then verify files


#### Library version errors during installation
- If using a rolling release or bleeding edge distro, try toggling `Prefer system libraries` in Lutris to `On`.


#### Installer Error Code 256 / Downloading [exe file] failed (ie arial32.exe)
- Try setting `Prefer system libraries` to `On` in global lutris options.
- Inspect install log for failed winetricks downloads or sha256 mismatch, note the URL of the files being downloaded and its destination in winetricks' cache.
- Download each file manually to its destination in winetricks' cache.
- Use winetricks to ensure that the prefix is set to Win10 mode.
- Proceed with lug-helper installer.


#### Lutris error: *Command exited with code 512*
- We suspect this is a Lutris bug and fixes seem inconsistent.
- Try going to Lutris Preferences -> Sources, and toggle either `Lutris` or `Local` and then toggle it back again.
- If you have an old install, try importing that into Lutris.


#### Lutris error: *"Runtime Error('No path can be generated for DXVK because no version information is available.')"*
- If you've just installed Lutris, be sure to launch it once, separately from the Star Citizen install process, to fully populate its runtime and caches.


#### RSI Launcher doesn't auto-update
- [Download](https://robertsspaceindustries.com/download) the latest launcher and install it by selecting `Run EXE inside Wine prefix` in Lutris:  
  ![Screenshot from 2023-05-11 10-33-19](https://github.com/starcitizen-lug/knowledge-base/assets/3657071/d146e9cc-e0a2-4327-acfb-ba5538ddefe4)

#### RSI Launcher error: *Could not fix permissions on directory*
- Please follow our [step-by-step guide](https://github.com/starcitizen-lug/knowledge-base/wiki/Tips-and-Tricks#rsi-launcher-20) for the 2.0 RSI Launcher

#### Installing Star Citizen on an NTFS-formatted drive
- Don't; it probably won't work and will likely only corrupt your game files.

***




## 💥 Crashes

#### RSI Launcher v1.6.2+ JavaScript error
- The LUG Helper's [wine installation](https://github.com/starcitizen-lug/knowledge-base/wiki/Quick-Start-Guide#installation-steps) method is recommended and avoids this error
- In the game's Lutris `System options`, make sure Advanced options is toggled on then in the `text-based games` section enable `CLI mode`
- Alternatively, select a Proton runner in Lutris' runner options tab, i.e. `ge-proton` and follow our [proton setup instructions](https://github.com/starcitizen-lug/knowledge-base/wiki/Tips-and-Tricks#proton)


#### Code 3 crash with error: *Star Citizen process exited abnormally (code: 3) : Command failed*
- You are likely missing 32bit drivers. See [32bit Drivers](#-32bit-drivers) below for more information
- Additionally, explicitly set the DXVK device name
  - identify device name using command `vulkaninfo --summary | grep deviceName`
  - set device name with environment variable `DXVK_FILTER_DEVICE_NAME=yourdevicenamehere`
- If using the Flatpak Lutris, you may need to resync it with your system after installing the 32bit drivers. Run: `flatpak update`


#### Game immediately crashes after clicking 'Launch'
- Start by checking the Wine output and/or "game.log" file
  
- See [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#general-news) for information on recent stability issues

- Possible cause: DXVK
  - Make sure DXVK is enabled in Lutris' Runner options.
  - Some people report changing their DXVK version fixes this. Try using our [Helper](https://github.com/starcitizen-lug/lug-helper) to download an async DXVK.
  - Nvidia users, check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) and Nvidia troubleshooting section [below](#-nvidia) for gpu driver issues, necessary workarounds, and currently recommended runner/DXVK versions.

- Possible cause: Incorrect Vulkan device
  - If you have Intel integrated graphics and see `VK_ICD_FILENAMES="/usr/share/vulkan/icd.d/intel_hasvk_icd.x86_64.json` in your log, then change the Vulkan device in Lutris to use your discrete GPU:
    - identify device name using command `vulkaninfo --summary | grep deviceName`
    - set device name with environment variable `DXVK_FILTER_DEVICE_NAME=yourdevicenamehere` 

- Possible cause: GPU drivers not working properly
  - If, in your "game.log", you see only `llvmpipe` listed as the working video adapter, your gpu drivers may not be functioning properly.
 
- Possible cause: Out of date flatpak libraries/packages
  - If you are using flatpak and have not run `flatpak update` recently, this should be done regularly to keep everything up to date.

- Possible cause: Phantom joystick
  - Many keyboards and mice can also have a "joystick" part in Linux, which Wine can detect. Unfortunately, Wine may be confused about it, as they are not real joysticks. In this case, the game could crash. Try running the Wine joystick control panel "wine control" (in Lutris: right click -> Joystick configuration) and disable your keyboard and/or mice.
  - This will not affect how your keyboard and mice work in the game.

- Possible cause: Linux kernel 6.8.9
   - Linux kernel 6.8.9 can result in a crash when launching from main menu, may be accompanied by a popup including text "Assertion failed!"
   - To fix: revert to kernel 6.8.8, update to 6.9+, or enable ReBar if your hardware supports it


#### Game crashes after clicking 'Verify'
- Make sure Star Citizen is installed on drive "C:\" Check the "Library Folder" option in the launcher settings:  
![Star Citizen launcher](https://media.discordapp.net/attachments/608349808956276737/927652866389340310/Screenshot_from_2022-01-03_14-56-37.png)
- Additionally, make sure the wine prefix is not installed on an NTFS formatted partition.


#### Game crashes with "STATUS_CRYENGINE_FATAL_ERROR" in game.log
- Some penguins have had success changing the Windows compatibility from Win10 to Win8.1 in the Wine configuration. Select Star Citizen in Lutris, then click the Wine button at the bottom and select `Wine configuration`:  
![](https://matrix-client.matrix.org/_matrix/media/r0/download/matrix.org/zKGOXxMOsktqYKqevqeSvYSw)  
- In the Wine configuration, under the `Applications` tab, change `Windows version` to `Windows 8.1`


#### Game crashes with "create_view: Assertion `!((UINT_PTR)base & page_mask)' failed" / "00adntdll:FILE_GetNtStatus Converting errno 12 to STATUS_UNSUCCESSFUL"
- Make sure you have set your vm.max_map_count as described in the installation section.


#### Crash or black screen while using Vulkan beta renderer
- Check the [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) recommendations for your graphics card
- Create a user.cfg file in the `{LIVE,PTU,TECH-PREVIEW}` directory and set `r.graphicsRenderer = 0`
 ```
 r.graphicsRenderer = 0
 ```


#### Failed to decompress file/corrupted block detected error
- Some Penguins have had this error when using BTRFS. We suspect a regression of some kind.
- Easiest: Just ignore the error and continue playing. It doesn't crash until you click the button.
- Or fix it: Disable CoW on the game's LIVE dir with `chattr +C ./LIVE`, then redownload or copy in a fresh data.p4k.
- Less easy Fix: Disable CoW only on the data.p4k file. This can only be done on an empty file.
- Alternatively, try mounting with the `compress` option instead of `compress-force`.
- If that doesn't work, switching to ext4 is an option.


#### After playing for a while, game/lutris/wine crash, no errors
  - If there are no errors in your game logs, check your system logs. It may be an Out Of Memory situation. Create a larger [swap file](Performance-Tuning#swap).


***




## 🧊 Freezes

#### Game hangs at splash screen or black/transparent window after clicking 'Launch'
- Make sure DXVK is enabled in Lutris' Runner options.
- Try changing to a different DXVK version in the Lutris settings.  Alternate DXVKs can be quickly installed using our [LUG Helper](https://github.com/starcitizen-lug/lug-helper).
- Nvidia users, check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for gpu driver issues, necessary workarounds, and currently recommended runner/DXVK versions.


#### Launcher freezes within a few seconds of opening
- Try using a different wine runner.
- Alternatively, you can try changing "Prefer system libraries" to ON:
  - Right click the game -> Configure -> System options -> Prefer system libraries


#### Launch Game stuck at "launching..."
- ⚠️ Launch Lutris in debug mode (`lutris -d`) and look for a `KeyError: 'contentstatsid'` error.
- If the error is present, check your Lutris version. This is fixed in v0.5.11. https://lutris.net/downloads


#### Launcher hangs / stops responding / crashes with an "ASAR" error
- Some people report the launcher hanging in combination with the Lutris runtime. If you are on Lutris, try toggling "Disable Lutris runtime" under "System options" of the Lutris game options.


***




## 🤪 Unexpected Behavior (sometimes also crashes)

#### Mouse/Cursor warp issues and view snapping in interaction mode
- The simplest workaround is to choose Xorg at your login screen instead of Wayland session. Other potential mitigations are:
  - Software cursor helps mitigate this for some. Create a user.cfg file in the LIVE, PTU, EPTU, TECH-PREVIEW directory
    ```
      #use software cursor
      pl_pit.forceSoftwareCursor = 1
    ```
  - [Proton](https://github.com/starcitizen-lug/knowledge-base/wiki/Alternative-Installations#proton-installation) helps mitigate this for some
  - Gamescope helps mitigate this for some
    - **Note for Nvidia users:** Gamescope may not work on your hardware. See [a possible fix below](#gamescope-not-working)
    - Install and enable gamescope. Set these options for your display resolution `-W 2560 -H 1440 --force-grab-cursor`
    - Other Gamescope settings that may be required depending on your system: `Window Mode` set to `Fullscreen` if it doesn't launch fullscreen, `-g` in `Custom Settings` to grab keyboard
    - Depending on your system, `Prefer System Libraries` may need to be enabled or disabled in Lutris
  - Wine wayland helps mitigate this for some
    - Add environment variable `DISPLAY=` to unset it to empty
    - Add RSI Launcher.exe argument ` --in-process-gpu`
  - Switching to an alternate desktop environment may help; most Gnome users don't seem to experience this issue
  - You may try building xwayland with [this patch](https://github.com/Nobara-Project/rpm-sources/blob/main/baseos/xorg-x11-server-Xwayland/xwayland-pointer-warp-fix.patch) applied. If using KDE and patching xwayland, you will also need to install Gamescope and use the `--force-grab-cursor` option


#### Mouse/Cursor restricted to a region smaller than the display, or clicks offset from cursor
- Create a user.cfg file in the LIVE, PTU, EPTU, TECH-PREVIEW directory
 ```
 #set to your display resolution
 r_width = 3440
 r_height = 1440
 ```


#### Empty launcher
- Log out log back in, or reset the launcher by pressing Ctrl+Shift+Alt+R


#### Visual glitches or semi-transparent lines, poor performance, possibly random crashes
- DXVK is likely disabled in Lutris's Runner options. Make sure it is enabled.
- Your game shader cache may need to be cleared. Our [Helper](https://github.com/starcitizen-lug/lug-helper) can quickly clear your game shaders.
![](https://media.discordapp.net/attachments/608349808956276737/1070664567425871960/SC_Lines.jpg)


#### No sound in game
- Depending on your distribution, you may need to set `Prefer System Libraries` in Lutris to `ON`.
- If you have sound in the launcher but not in the game, launch the game and go to your audio settings, then enable "Play sound while game is in background".


#### Anticheat encountered an error (possible code 30033, 30034)
- Please follow [our EAC migration instructions](https://github.com/starcitizen-lug/knowledge-base/wiki/Tips-and-Tricks#easy-anti-cheat)
- Check your process list for any lingering wine processes. Reboot if necessary.
- You may have to delete the EAC directory in youre prefix's `AppData/Roaming` directory.
- You may also have to delete the EAC directory in the Star Citizen `LIVE` directory, followed by verifying files in the launcher.


#### Required Vulkan Extensions are missing error / poor performance compared to windows / error code 3
- Check if you have amdvlk installed by running `vulkaninfo --summary`. The vulkaninfo utility is part of the package `vulkan-tools` on most distros. You can also check your package manager.
- If your system is using amdvlk, uninstall that package and replace it with `vulkan-radeon`.
- For additional help with this, ask in our [Discord](https://github.com/starcitizen-lug/knowledge-base/wiki#welcome-space-penguins) tech support channel.


#### DirectX error message
- Error may read "Star Citizen requires DirectX feature level of 11.1 as a minimum which is not supported at present on this machine"  
  ![image](https://user-images.githubusercontent.com/3657071/224719841-ba1e831b-4ace-4f14-b423-3e49528154c6.png)
- Check that the `Vulkan device` is not set to an integrated gpu (ie, Intel)
  - identify device name using command `vulkaninfo --summary | grep deviceName`
  - set device name with environment variable `DXVK_FILTER_DEVICE_NAME=yourdevicenamehere`
  - verify by setting environment variable `DXVK_HUD=1` and observing the device name in the upper left of the screen
- Also make sure your GPU drivers (Mesa/nvidia) are up to date and DXVK is enabled/updated.


#### Failed to initialize dependencies error
- Make sure the `SDL_VIDEODRIVER` environment variable is **NOT** set globally to `wayland` on your system: `env | grep SDL_VIDEODRIVER`
- If it is set, remove it from whichever environment config(s) is setting it.


#### Black or flickering window, possible crash with errors 15006 or 30007
- Check for larger resolutions and scaling settings.  See CIG's [support article](https://support.robertsspaceindustries.com/hc/en-us/articles/360000081887-Guide-to-Graphic-Issues#large-res)


#### Black/transparent window after clicking 'Launch'
- Check our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for gpu driver issues, necessary workarounds, and currently recommended runner/DXVK versions.
- Make sure DXVK is enabled in Lutris' Runner options.
- Try changing to a different DXVK version in the Lutris settings.  Alternate DXVKs can be quickly installed using our [LUG Helper](https://github.com/starcitizen-lug/lug-helper).


#### RSI Launcher white screen / error DCompositionCreateDevice
- In Lutris, configure Star Citizen (right-click->Configure->Game options) and add `"--use-gl=osmesa"` to the Arguments field.
- If launching manually: `wine "RSI Launcher.exe" "--use-gl=osmesa"`
 

#### RSI Launcher fails to launch from lutris with CLI mode enabled
- Error message may be similar to `/usr/bin/gnome-terminal.real: symbol lookup error: /lib/x86_64-linux-gnu/libatk-bridge-2.0.so.0: undefined symbol: atk_component_scroll_to`
- Disable the lutris runtime in lutris global preferences to work around this error


#### Non-US keyboard keys not working
- Check the [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#general-news) and use the LUG Helper "manage runners" options to select a recent staging wine
- In a terminal run `./sc-launch.sh shell` then `winecfg`
- Select your language from the list and enable scancode auto-detection
    ![staging_input_menu](https://github.com/user-attachments/assets/a525f310-3a2a-49b1-bb6e-c07875e15608)
- If the above doesn't fix it, you can try setting the `LANG=` environment variable. For example, `LANG=de_DE`


***




## 💚 Nvidia

#### Current known issues
- See the Nvidia section of our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news) for the ways in which Nvidia is being special today.

#### Crash when taking shield damage in-game
- There is a shield rendering bug that causes the game to crash. It seems to affect 1000 series cards.
- There is currently no known workaround other than switching cards. We recommend AMD.

#### Popup saying your Nvidia graphics driver is out of date
- Ignore or Disable DXVK NVAPI in Lutris.
  - Right click the game -> Configure -> Runner options -> Enable DXVK-NVAPI/DLSS (set to off)

#### Game fails to start after clicking Launch Game on laptops with Nvidia GPU + intel graphics
- Errors may include `DXVAVDA fatal error: could not LoadLibrary: msvproc.dll` or `Major opcode of failed request:  156 (NV-GLX)`
- Try removing all optimus/prime env vars for render offload and set the Vulkan device to the Nvidia GPU.
  - identify device name using command `vulkaninfo --summary | grep deviceName`
  - set device name with environment variable `DXVK_FILTER_DEVICE_NAME=yourdevicenamehere`

#### Severe frame drops
- Some Penguins are seeing VRAM exhaustion problems on nvidia cards. It appears to be driver related and does not seem to affect AMD cards.
- A workaround that some Penguins have had some success with:
   - Create a new `dxvk.conf` file and add `d3d11.cachedDynamicResources = "a"` to it, then either export `DXVK_CONFIG_FILE=path/to/dxvk.conf` or, if using Lutris, add `DXVK_CONFIG_FILE` as a new environment variable in the game's settings and set it to the file path.
   - If you still have issues or are running applications like OBS, you may also have to limit the vram the game sees to free up some vram for other applications. For example:
      - Card with 8GB vram: `dxgi.maxDeviceMemory = 6144`
      - Card with 6GB vram: `dxgi.maxDeviceMemory = 4096`

#### Vulkan Beta: Game fails to launch
- There is an [issue with LibCUDA](https://github.com/jp7677/dxvk-nvapi/issues/174#issuecomment-2227462795) that prevents vulkan and DLSS from working on linux.
- If using Wine-GE, add the environment variable `WINE_HIDE_NVIDIA_GPU=1` to enable vulkan
- If using Wine or Wine-GE, see [instructions](https://github.com/starcitizen-lug/knowledge-base/wiki/Troubleshooting#dlssdeep-learning-super-sampling--vulkan) to patch libcuda to enable both vulkan and DLSS 
 
#### DLSS(Deep Learning Super Sampling) / Vulkan
- There is a [memory allocation issue with LibCUDA](https://github.com/jp7677/dxvk-nvapi/issues/174#issuecomment-2227462795), where it attempts to allocate in a specific area already occupied by the game.
   - A possible solution would be patching LibCUDA file increasing this area.
      - Locate your 64-bit `libcuda.so` (usually `/usr/lib` or run `whereis libcuda.so`).
      - To generate `libcuda.patched.so`, replace both placeholder `/path/to/` lines below then run:  
        ```
        echo -ne $(od -An -tx1 -v /path/to/libcuda.so | tr -d '\n' | sed -e 's/00 00 00 f8 ff 00 00 00/00 00 00 f8 ff ff 00 00/g' -e 's/ /\\x/g') > /desired/path/to/libcuda.patched.so
        ```
      - Use the environment variable `LD_PRELOAD` to load the patched version:  
       `LD_PRELOAD=/path/to/the/libcuda.patched.so:$LD_PRELOAD`
      - Remove the `WINE_HIDE_NVIDIA_GPU` env variable if it is set in Lutris or your launch script.
      - Don't forget to enable DXVK-NVAPI.

#### Gamescope not working
- See this [known issue report](https://github.com/ValveSoftware/gamescope/issues/526).
- A possible fix is to set the environment variable `__GL_THREADED_OPTIMIZATIONS=0`
   - Lutris: `Right click the game->Configure->System options->Game execution->Environment variables` then find or create `__GL_THREADED_OPTIMIZATIONS` in the left column and change/set it to `0` in the right column.
   - Non-Lutris: Edit the `sc-launch.sh` script installed by the Helper in your prefix (ie, `~/Games/star-citize/sc-launch.sh`) and add `export __GL_THREADED_OPTIMIZATIONS=0` to the environment variables.


***




## 💖 AMD

#### Current known issues
- See the AMD section of our [latest news](https://github.com/starcitizen-lug/knowledge-base/wiki#news)

#### Vulkan Beta: Bright flickering lights at edges of in-game display panels
- To fix: Add environment variable `radv_zero_vram=true`

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
