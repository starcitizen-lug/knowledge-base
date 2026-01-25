---
title: "💚 Nvidia"
description: "Known issues and troubleshooting steps for Nvidia users running Star Citizen on Linux"
parent: "Troubleshooting"
nav_order: 7
md_message: "You are viewing raw source files... Go to https://wiki.starcitizen-lug.org/ to use the wiki!"
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
- Some Penguins are seeing VRAM exhaustion problems on Nvidia cards. Overriding the max allowed VRAM allocation may help.
- Use the LUG Helper to [edit your launch script](/Tips-and-Tricks#how-to-edit-the-launch-script).
- **If you're using DXVK:**
  - Add the following environment variable to your [launch script](/Tips-and-Tricks#how-to-edit-the-launch-script). Replace `4096` with the appropriate value from the table below.
  ```
  export DXVK_CONFIG="dxgi.maxDeviceMemory = 4096;cachedDynamicResources = a;"
  ```
- **If you're using Vulkan:**
  - Use `vulkaninfo --summary` to verify that you have the `VK_LAYER_MESA_vram_report_limit` layer available. If you do not, then use your package manager to install `vulkan-mesa-layers` or similar.
  - Use `vulkaninfo --summary` to find the correct `vendorID:deviceID` values for your GPU.
  - Add the following environment variables to your [launch script](/Tips-and-Tricks#how-to-edit-the-launch-script). Replace `4096` with the appropriate value from the table below. Replace `ID=0x1002:0x73df` with the `vendorID:deviceID` values found above.
  ```
  export VK_LOADER_LAYERS_ENABLE=VK_LAYER_MESA_vram_report_limit
  export VK_VRAM_REPORT_LIMIT_HEAP_SIZE=4096
  export VK_VRAM_REPORT_LIMIT_DEVICE_ID=0x1002:0x73df
  ```

  | GPU VRAM (GB)    | Overriden Value (MB) |
  | ------------- | ------------- |
  | 12 | 9216 |
  | 10 | 8192 |
  | 8  | 6144 |
  | 6  | 4096 |
  | 4  | 2048 |


## DLSS (Deep Learning Super Sampling)
1. Use the latest [LUG Helper](/Tips-and-Tricks#how-to-run-the-lug-helper) to install a LUG-Wine runner. (For any other wine runners, avoid wine-staging)
2. Use the latest [LUG Helper](/Tips-and-Tricks#how-to-run-the-lug-helper), select `Manage DXVK`, and install `DXVK-NVAPI`
3. DLSS 3 will now be available in the game options
4. To enable DLSS 4.0, add the following environment variables to your [launch script](/Tips-and-Tricks#how-to-edit-the-launch-script).

   ```
   export PROTON_ENABLE_NGX_UPDATER="1" 
   export DXVK_NVAPI_DRS_NGX_DLSS_SR_OVERRIDE="on"
   export DXVK_NVAPI_DRS_NGX_DLSS_RR_OVERRIDE="on"
   export DXVK_NVAPI_DRS_NGX_DLSS_FG_OVERRIDE="on"
   export DXVK_NVAPI_DRS_NGX_DLSS_SR_OVERRIDE_RENDER_PRESET_SELECTION="RENDER_PRESET_K"
   export DXVK_NVAPI_DRS_NGX_DLSS_RR_OVERRIDE_RENDER_PRESET_SELECTION="RENDER_PRESET_K"
   ```

{: .note-title }
> DLSS 4.5
> 
> Enabling DLSS 4.5 will result in less performance than DLSS 4.0 in exchange for improved image quality. [RTX 20 & 30 series GPUs](https://www.nvidia.com/en-us/geforce/forums/geforce-graphics-cards/5/580689/dlss-45-super-resolution-faq/) will see a very severe performance impact and should stick with DLSS 4.0.
> 
> Enable DLSS 4.5 by using an alternative render preset:
> - `RENDER_PRESET_M` for improved image quality but less performance.
> - `RENDER_PRESET_L` for the best image quality but the least performance.

5. To confirm DLSS 4.x is working, enable the debug overlay env var below. Look for it in-game to say `Render Preset: K/M/L`, `DLSSv3 v310.4.0` for DLSS 4.0, or `DLSSv3 v310.5.0` for DLSS 4.5.
   ```
   export DXVK_NVAPI_SET_NGX_DEBUG_OPTIONS="DLSSIndicator=1024,DLSSGIndicator=2"
   ```
6. Disable the debug overlay when done by changing the above env var to:
   ```
   export DXVK_NVAPI_SET_NGX_DEBUG_OPTIONS="DLSSIndicator=1,DLSSGIndicator=1"
   ```


## Nvidia Smooth Motion
- To enable Smooth Motion on supported cards, use the LUG Helper to [edit your launch script](/Tips-and-Tricks#how-to-edit-the-launch-script), then add the following environment variable:
  ```
  export NVPRESENT_ENABLE_SMOOTH_MOTION=1
  ```
- To [use Mangohud alongside Smooth Motion](https://forums.developer.nvidia.com/t/580-release-feedback-discussion/341205/329), also add the following env var:
  ```
  export NVPRESENT_QUEUE_FAMILY=1
  ```

{: .warning }
>
> - Mangohud and other FPS monitoring HUDS may interfere with Smooth Motion and cause game crashes. You may need to disable them.
> - Vsync may need to be disabled in the game's graphics settings.

{: .tip }
> When using Smooth Motion, the following environment variables may slightly improve latency if you have a compatible monitor:
> ```
> export __GL_GSYNC_ALLOWED=1
> export __GL_MaxFramesAllowed=1
> ```


## Gamescope not working
- See this [known issue report](https://github.com/ValveSoftware/gamescope/issues/526).
- A possible fix is to set the environment variable `__GL_THREADED_OPTIMIZATIONS=0`
