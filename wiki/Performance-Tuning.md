## LUG Helper
We have a helper script which can help you manage and optimize Star Citizen on Linux. It can check/set recommended settings such as vm.max_map_count and the system's open file descriptors limit, manage Lutris runners and DXVK versions, delete your Star Citizen USER directory while preserving keybinds, and delete shaders or dxvk cache for troubleshooting purposes. It can be downloaded from:

https://github.com/starcitizen-lug/lug-helper

## DXVK Async
Using an async DXVK can greatly reduce stuttering.  
We recommend https://github.com/Sporif/dxvk-async/ (Nvidia users, see our [latest news](https://github.com/starcitizen-lug/information-howtos/wiki#news))  
You can manually download it into the Lutris dxvk directory or use the Helper to automatically install it  
After downloading, be sure to set the environment variable `DXVK_ASYNC=1` and enable the downloaded version in the Lutris runner options.
1. `Right click the game->Configure->System options->Environment variables`. Add `DXVK_ASYNC` as the key and `1` as the value.
2. `Right click the game->Configure->Runner Options`. Check `Show advanced options` to unhide `DXVK version`.
3. In `DXVK version`, select `Manual` then overwrite it with the folder name of the downloaded dxvk (ie. _dxvk-async-1.9.4_)

![](https://matrix-client.matrix.org/_matrix/media/r0/download/matrix.org/wQRsUySnKmchQWyZrmoZFDnJ)

## Nvidia Cache

By default Nvidia has a combined cache for all games. As the cache fills up from other games, Star Citizen's shaders may get deleted leading to poor FPS. We recommend giving SC its own persistent cache by adding the following environment variables:

```
__GL_SHADER_DISK_CACHE=true
__GL_SHADER_DISK_CACHE_PATH="/path/you/want/for/your/cache"  (example: /home/myuser/.cache/sccache)
__GL_SHADER_DISK_CACHE_SKIP_CLEANUP=true
```

If you use Lutris, these environment variables can be added here:

`Right click the game->Configure->System options->Environment variables`

![](https://matrix-client.matrix.org/_matrix/media/r0/download/xndr.de/AwspONZSbLKcXCCkBojwyIYT)

## Game Settings

The following game settings can help improve framerates:

- Set `Quality` to `High`. Lower settings are not recommended as it will tax your CPU more. Set to `Very High` to offload more work from your CPU to your GPU.
- Set `Planet Volumetric Clouds` to `Medium`
- Set `Scattered Object Distance` to `Low`
- Set `Motion Blur` to `Off`
- Set `Sharpening` to `100`

## Feral GameMode

Gamemode can help improve performance by applying OS-level performance tweaks as the game is launched. Search for `gamemode` in your Distro's repos. Once installed, Lutris has a toggle for `Enable Feral GameMode` under `System options`. It defaults to ON if it detects gamemode is installed.

## Fsync

An fsync-enabled Kernel can help improve smoothness while shaders are being compiled in the game. Enable fsync in Lutris under Runner Options.

## Zram & Swap

Zram stores swap in RAM using on-the-fly compression which can improve game performance when memory utilization gets high.
- For systems with 16GB RAM, we recommend all 16GB configured for zram with at least an 8GB swap file.
- For systems with 32GB RAM or more, zram can be used in place of a swap file as long as there is at least a total of 40GB combined RAM + swap.

See the [Arch Wiki](https://wiki.archlinux.org/title/Zram) for configuration instructions that should work for most distros.

If you prefer not to use zram, swap files will need to be configured. We recommend configuring at least a combined 40GB RAM + swap:
- For 16GB RAM: 24GB swap
- For 32GB RAM: 8GB swap

More swap should be configured if you intend to run a few background applications while playing the game.

## Steam Deck

We recommend a 16gb swap file for the Steam Deck. Create it under `/home` instead of `/` to protect it from being wiped out by SteamOS updates.

## Changing CPU scaling behavior via the Linux kernel and System Management BIOS

To achieve a more stable framerate in Star Citizen, ideally you will want a stable CPU frequency. There are [several schedulers](https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt) provided by the Linux kernel. Start with the `Performance` scheduler to hint that the CPU should always run at the maximum frequency before trying the demand-based schedulers.

We have discovered that Dell laptops with Intel CPUs (and possibly other mobile hardware configurations) may have other factors that influence CPU frequency scaling:
- In situations where one of these laptops is either thermal-limited or power-limited, the CPU and GPU will set the maximum frequency and then fall to a low frequency (ie. 800 MHz) when it hits the limit.
- You can try to configure these settings in the BIOS or via [SMBIOS](https://www.dmtf.org/standards/smbios). On Ubuntu distributions, this utility is provided by the `smbios-utils` package.

**Solution for affected laptops:**

If changing the kernel scheduler between `Performance` and the various demand-based schedulers doesn't affect CPU frequency scaling for your laptop, try setting the SMBIOS thermal mode to `cool-bottom`. This mode behaves similarly to the `Conservative` kernel governor, gradually incrementing/decrementing the CPU frequency to stabilize the framerate.
- Using the SMBIOS utility on Ubuntu, the command is `sudo smbios-thermal-ctl --set-thermal-mode=cool-bottom`

## Increased performance for CPUs with multiple dies
### Affected CPU generations
- Amd Threadripper
### Steps
1. Verify you have a CPU with multiple dies by running `lstopo`. If the results appear similar to the first image below, you can proceed:  
    ![image](https://user-images.githubusercontent.com/39007301/220378862-d4b9bbd7-15b3-4e1e-b77d-6b19f0908ba8.png)  
    
    If, on the other hand, your CPU is like this image where the dies are not shown, this will not improve your performace:  
    <img src="https://user-images.githubusercontent.com/39007301/220378475-160e9091-3b2c-407b-acff-d606892d21c5.png" width=60% height=60%>  

2. Modify the following environment variable to match your system:  
    ```
    WINE_CPU_TOPOLOGY=Number_of_Threads:List_of_threads_indexes
    ```
    The `Number_of_threads` is the number of threads you want to run Star Citizen with.  
    The `List_of_thread_indexes` can be determined by looking at the `lstopo` output.  
    You can see the threads highlighted in the image below:  
    <img src="https://user-images.githubusercontent.com/39007301/220380665-5378ccc5-474e-4db2-8a4a-e893bb4ab347.png" width=60% height=60%>  

    As an example, the CPU shown below would end up with the arguments  
    ```
    WINE_CPU_TOPOLOGY=16:0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15
    ```
    ![image](https://user-images.githubusercontent.com/39007301/220382182-3525c3e8-4466-4489-8e85-7c1319ac3a1b.png)

3. Run the game with the modified environment variable. If using Lutris, add the modified environment variable as shown in the image below:
    `Right click the game->Configure->System options->Environment variables`

    ![220531210-be82dc26-696f-4748-83ce-7161c362fe0b](https://user-images.githubusercontent.com/3657071/225932793-2f46c08b-47f1-4087-8f13-4e5cfd976837.png)


    
