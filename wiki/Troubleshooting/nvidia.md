---
title: "💚 Nvidia"
parent: "Troubleshooting"
nav_order: 4
---

# 💚 Nvidia

## Current known issues
- See the Nvidia section of our [latest news](/#news) for the ways in which Nvidia is being special today.

## Crash when taking shield damage in-game
- There is a shield rendering bug that causes the game to crash. It seems to affect 1000 series cards.
- There is currently no known workaround other than switching cards. We recommend AMD.

## Popup saying your Nvidia graphics driver is out of date
Typically caused by dxvk being broken or not installed
- Use the LUG Helper to update dxvk

## Game fails to start after clicking Launch Game on laptops with Nvidia GPU + intel graphics
- Errors may include  
`DXVAVDA fatal error: could not LoadLibrary: msvproc.dll`  
or  
`Major opcode of failed request:  156 (NV-GLX)`
- Try removing all optimus/prime env vars for render offload and set the Vulkan device to the Nvidia GPU.
  - identify device name using command `vulkaninfo --summary | grep deviceName`
  - set device name with environment variable `DXVK_FILTER_DEVICE_NAME=yourdevicenamehere`

## Severe frame drops
- Some Penguins are seeing VRAM exhaustion problems on nvidia cards
- [Add a new](/Tips-and-Tricks#how-to-edit-the-launch-script) `DXVK_CONFIG` environment variable to override the max device memory.  
  Refer to [DXVK config](https://github.com/doitsujin/dxvk/blob/master/dxvk.conf) for examples
   - Card with 12GB vram
   ```
   export DXVK_CONFIG="dxgi.maxDeviceMemory = 9216;cachedDynamicResources = a;"
   ```
   - Card with 10GB vram
   ```
   export DXVK_CONFIG="dxgi.maxDeviceMemory = 8192;cachedDynamicResources = a;"
   ```
   - Card with  8GB vram
   ```
   export DXVK_CONFIG="dxgi.maxDeviceMemory = 6144;cachedDynamicResources = a;"
   ```
   - Card with  6GB vram
   ```
   export DXVK_CONFIG="dxgi.maxDeviceMemory = 4096;cachedDynamicResources = a;"
   ```
   - Card with  4GB vram
   ```
   export DXVK_CONFIG="dxgi.maxDeviceMemory = 2048;cachedDynamicResources = a;"
   ```


## DLSS (Deep Learning Super Sampling)
1. Use the latest [LUG Helper](https://github.com/starcitizen-lug/lug-helper/releases) to install a standard (non-staging) LUG-Wine runner. (For wine-staging: there is a memory allocation issue with libcuda + wine-staging and Easy Anti-Cheat makes this prohibitively difficult to overcome)
2. Install winetricks `20250102-next` or newer. System winetricks can be updated with  
   `sudo winetricks --self-update`
3. Enter a [Wine maintenance shell](/Tips-and-Tricks#how-to-get-a-wine-maintenance-shell-using-the-launch-script) for your prefix using the `sc-launch.sh` script.
4. Install `dxvk` >=2.6.2 and `dxvk_nvapi` >=0.9 into your wine prefix with the following command:
   1. `winetricks -f dxvk dxvk_nvapi`
   2. Note: If you do not use the Helper's Wine maintenance shell, you'll need to prepend `WINEPREFIX=/path/to/star-citizen/prefix` to the above command!
5. To enable DLSS 4, add the following environment variables. In the Helper's Maintenance menu, select the `Edit launch script` option
   ```
   export PROTON_ENABLE_NGX_UPDATER="1" 
   export DXVK_NVAPI_DRS_NGX_DLSS_SR_OVERRIDE="on"
   export DXVK_NVAPI_DRS_NGX_DLSS_RR_OVERRIDE="on"
   export DXVK_NVAPI_DRS_NGX_DLSS_FG_OVERRIDE="on"
   export DXVK_NVAPI_DRS_NGX_DLSS_SR_OVERRIDE_RENDER_PRESET_SELECTION="render_preset_latest"
   export DXVK_NVAPI_DRS_NGX_DLSS_RR_OVERRIDE_RENDER_PRESET_SELECTION="render_preset_latest"
   ```
6. To confirm DLSSv4 is working, enable the debug overlay env var and look for it in-game to say `Render Preset: K` or `DLSSv3 v310.x+`
   ```
   export DXVK_NVAPI_SET_NGX_DEBUG_OPTIONS="DLSSIndicator=1024,DLSSGIndicator=2"
   ```
7. Disable the debug overlay when done by changing the above env var to:
   ```
   export DXVK_NVAPI_SET_NGX_DEBUG_OPTIONS="DLSSIndicator=1,DLSSGIndicator=1"
   ```
8. Note that nvidia driver v575 may be unstable. v570 is recommended for stability.


## Gamescope not working
- See this [known issue report](https://github.com/ValveSoftware/gamescope/issues/526).
- A possible fix is to set the environment variable `__GL_THREADED_OPTIMIZATIONS=0`
