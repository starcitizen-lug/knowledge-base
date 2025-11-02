---
title: "💚 Nvidia"
description: "Known issues and troubleshooting steps for Nvidia users running Star Citizen on Linux"
parent: "Troubleshooting"
nav_order: 7
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
- Some Penguins are seeing VRAM exhaustion problems on Nvidia cards
- One way to fix the problem is to [add a new set of environment variables in the Star Citizen launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) that override the maximum allowed VRAM allocation on the GPU
- Here are some recommended values:

| GPU VRAM (GB)    | Overriden Value (MB) |
| ------------- | ------------- |
| 16 | 12288 |
| 12 | 9216 |
| 10 | 8192 |
| 8  | 6144 |
| 6  | 4096 |
| 4  | 2048 |
| 2  | 1024 |

- You may experiment with different values, but opting for the recommendation is likely to yield the best performance result with the least tinkering

> [!NOTE]
> After making this change, Star Citizen will still use the GPU's entire amount of VRAM. Overriding the maximum allotment simply overcomes a problem with VRAM allocation on Nvidia GPUs in GNU/Linux. In other words, doing this optimizes the GPU's performance.

### DXVK
Refer to [DXVK config](https://github.com/doitsujin/dxvk/blob/master/dxvk.conf) for examples.

The simplest format/solution is to add this single environment variable to your launch script:

```
export DXVK_CONFIG="dxgi.maxDeviceMemory = 4096;cachedDynamicResources = a;"
```
Replace the sample '4096' value with the recommended overriden value shown above for the amount of VRAM that your GPU has.

### Vulkan
Use `vulkaninfo --summary` to verify that you have the `VK_LAYER_MESA_vram_report_limit` Vulkan layer available. If you do not, your particular GNU/Linux distribution might have it packaged for you to install. When you do, then you should add the following three environment variables to your launch script:

```
export VK_LOADER_LAYERS_ENABLE=VK_LAYER_MESA_vram_report_limit
```
```
export VK_VRAM_REPORT_LIMIT_HEAP_SIZE=4096
```
Replace the sample '4096' value with the recommended overriden value shown above for the amount of VRAM that your GPU has.
```
export VK_VRAM_REPORT_LIMIT_DEVICE_ID=0x1002:0x73df
```
`ID=` takes the format `vendorID:deviceID`. Use `vulkaninfo --summary` to find out what this should be for your GPU.

## DLSS (Deep Learning Super Sampling)
1. Use the latest [LUG Helper](/Tips-and-Tricks#how-to-run-the-lug-helper) to install a LUG-Wine runner. (For any other wine runners, avoid wine-staging)
2. Use the latest [LUG Helper](/Tips-and-Tricks#how-to-run-the-lug-helper), select `Manage DXVK`, and install `DXVK-NVAPI`
3. DLSS 3 will now be available in the game options
4. To enable DLSS 4, add the following environment variables. In the Helper's Maintenance menu, select the `Edit launch script` option
   ```
   export PROTON_ENABLE_NGX_UPDATER="1" 
   export DXVK_NVAPI_DRS_NGX_DLSS_SR_OVERRIDE="on"
   export DXVK_NVAPI_DRS_NGX_DLSS_RR_OVERRIDE="on"
   export DXVK_NVAPI_DRS_NGX_DLSS_FG_OVERRIDE="on"
   export DXVK_NVAPI_DRS_NGX_DLSS_SR_OVERRIDE_RENDER_PRESET_SELECTION="render_preset_latest"
   export DXVK_NVAPI_DRS_NGX_DLSS_RR_OVERRIDE_RENDER_PRESET_SELECTION="render_preset_latest"
   ```
5. To confirm DLSSv4 is working, enable the debug overlay env var and look for it in-game to say `Render Preset: K` or `DLSSv3 v310.x+`
   ```
   export DXVK_NVAPI_SET_NGX_DEBUG_OPTIONS="DLSSIndicator=1024,DLSSGIndicator=2"
   ```
6. Disable the debug overlay when done by changing the above env var to:
   ```
   export DXVK_NVAPI_SET_NGX_DEBUG_OPTIONS="DLSSIndicator=1,DLSSGIndicator=1"
   ```


## Gamescope not working
- See this [known issue report](https://github.com/ValveSoftware/gamescope/issues/526).
- A possible fix is to set the environment variable `__GL_THREADED_OPTIMIZATIONS=0`
