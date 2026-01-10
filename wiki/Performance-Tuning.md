---
title: "Performance Tuning"
description: "Suggestions for improving the performance of Star Citizen on Linux"
nav_order: 4
md_message: "You are viewing raw source files... Go to https://wiki.starcitizen-lug.org/ to use the wiki!"
---
# Performance Tuning

## LUG Helper
The [LUG Helper](Tips-and-Tricks.md#how-to-run-the-lug-helper)'s Preflight Check will do a quick check of your system for some common issues. Be sure it passes all checks.


## Game Settings

The following game settings can help improve framerates:

- Set `Quality` to `High`. Lower settings are not recommended as it will tax your CPU more. Set to `Very High` to offload more work from your CPU to your GPU.
- Set `Planet Volumetric Clouds` to `Medium`
- Set `Object View Distance` to `Low`
- Set `Motion Blur` to `Off`
- Set `Sharpening` to `100`


## Zram & Swap

We currently recommend a combined 40GB RAM + swap to avoid Out Of Memory crashes while playing Star Citizen. Systems with less than 40GB RAM will need additional swap or zram configured. Systems with >40GB RAM should be fine as long as any size swap file exists; the game likes to swap even when you have plenty of ram.

Zram stores swap in RAM using on-the-fly compression which can improve game performance when memory utilization gets high. In our experience, this tends to provide better performance in Star Citizen than zswap.
- For systems with 16GB RAM, we recommend all 16GB configured for zram with at least 8-16GB in a swap file.
- For systems with 32GB RAM, we recommend configuring all 32GB for zram with at least 4-8GB in a swap file.

{: .tip }
> - When using zram, zswap needs to be [disabled](https://wiki.archlinux.org/title/Zswap#Toggling_zswap).  
> - See the Arch Wiki for [zram setup](https://wiki.archlinux.org/title/Zram#Using_zram-generator) instructions that should work for most distros as well as [zram optimization](https://wiki.archlinux.org/title/Zram#Optimizing_swap_on_zram) steps.  
> - Also see the Arch Wiki for [swap file creation](https://wiki.archlinux.org/title/Swap#Swap_file_creation) instructions.  

The zram-generator package requires a configuration file. Many distros use zram by default, edit the existing or create your own based on this example:
```
## /etc/systemd/zram-generator.conf

[zram0]
zram-size = ram
compression-algorithm = zstd
```

If you prefer not to use zram, a swap file will need to be [configured](https://wiki.archlinux.org/title/Swap#Swap_file). Btrfs users please follow the [Btrfs instructions](https://wiki.archlinux.org/title/Btrfs#Swap_file). We recommend configuring at least a combined 40GB RAM + swap:
- For 16GB RAM: 24GB swap
- For 32GB RAM: 8GB swap

{: .important }
>
> More swap should be configured if you intend to run background applications while playing the game.


## ESync/FSync/NTSync

{: .tip }
> If you've installed the game via our [LUG Helper](Tips-and-Tricks.md#how-to-run-the-lug-helper), these settings are pre-configured for you.

- If these environment variables are set, Wine will automatically choose the best option between esync or fsync.
  ```
  export WINEESYNC=1
  export WINEFSYNC=1
  ```
- `NTSync` requires kernel 6.14+ and a wine 10.16 or newer which can be easily [installed](Tips-and-Tricks#how-to-add-a-wine-runner) using the LUG Helper. No additional environment variables are needed.


## Nvidia Cache

{: .tip }
> If you've installed the game via our [LUG Helper](Tips-and-Tricks.md#how-to-run-the-lug-helper), these settings are pre-configured for you.

By default Nvidia has a combined cache for all games. As the cache fills up from other games, Star Citizen's shaders may get deleted leading to poor FPS. We recommend giving SC its own persistent cache by adding the following environment variables:
```
__GL_SHADER_DISK_CACHE=true
__GL_SHADER_DISK_CACHE_PATH="/path/you/want/for/your/cache"  (example: /home/games/star-citizen/nvidiacache)
__GL_SHADER_DISK_CACHE_SKIP_CLEANUP=true
```


## Mesa (AMD/Intel) Shader Cache

{: .tip }
> If you've installed the game via our [LUG Helper](Tips-and-Tricks.md#how-to-run-the-lug-helper), these settings are pre-configured for you.

Mesa can be given its own persistent shader cache by adding the following environmental variables:
```
MESA_SHADER_CACHE_DIR="/path/you/want/for/your/cache"  (example: /home/games/star-citizen/amdcache)
MESA_SHADER_CACHE_MAX_SIZE=10G
```


## Feral GameMode

For most configurations, Gamemode does not seem to result in significant performance benefits. If you wish to experiment with its capabilities, install `gamemode` from your package manager, then refer to the Gamemode [repository](https://github.com/FeralInteractive/gamemode) for configuration instructions.

Use the LUG Helper to [edit your launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) and add `gamemoderun` to the beginning of your launch command.


## CPU scaling on Laptops

When configuring kernel [schedulers](https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt) on a mobile device, the `Performance` scheduler will hint that the CPU should always run at the maximum frequency.

Dell laptops with Intel CPUs may have other factors that influence CPU frequency scaling:
- If the laptop is thermal-limited or power-limited, the CPU and GPU will fall to a lower frequency when it hits the limit.
- You can try to configure these settings in the BIOS or via [SMBIOS](https://www.dmtf.org/standards/smbios). On Ubuntu distributions, this utility is provided by the `smbios-utils` package.

**Solution for affected laptops:**

If changing the kernel scheduler between `Performance` and the various demand-based schedulers doesn't affect CPU frequency scaling for your laptop, try setting the SMBIOS thermal mode to `cool-bottom`. This mode behaves similarly to the `Conservative` kernel governor, gradually incrementing/decrementing the CPU frequency to stabilize the framerate.
- Using the SMBIOS utility on Ubuntu, the command is `sudo smbios-thermal-ctl --set-thermal-mode=cool-bottom`

## Increased performance for CPUs with multiple dies
**Affected CPU generations:**
- Amd Threadripper

**Steps**
1. Verify you have a CPU with multiple dies by running `lstopo`. If the results appear similar to the first image below, you can proceed:  
    ![CPU Topology](https://user-images.githubusercontent.com/39007301/220378862-d4b9bbd7-15b3-4e1e-b77d-6b19f0908ba8.png){: style="display: block;max-height: 300px;" }

    If, on the other hand, your CPU is like this image where the dies are not shown, this will not improve your performace:  
    ![CPU Topology](https://user-images.githubusercontent.com/39007301/220378475-160e9091-3b2c-407b-acff-d606892d21c5.png){: style="display: block;max-height: 300px;" }
2. Modify the following environment variable to match your system:  
    ```
    WINE_CPU_TOPOLOGY=Number_of_Threads:List_of_threads_indexes
    ```
    The `Number_of_threads` is the number of threads you want to run Star Citizen with.  
    The `List_of_thread_indexes` can be determined by looking at the `lstopo` output.  
    You can see the threads highlighted in the image below:  
    ![CPU Topology](https://user-images.githubusercontent.com/39007301/220380665-5378ccc5-474e-4db2-8a4a-e893bb4ab347.png){: style="display: block;max-height: 300px;" }

    Run the game with the modified environment variable. As an example, the CPU shown below would end up with the arguments  
    ```
    WINE_CPU_TOPOLOGY=16:0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15
    ```
    ![CPU Topology](https://user-images.githubusercontent.com/39007301/220382182-3525c3e8-4466-4489-8e85-7c1319ac3a1b.png)
