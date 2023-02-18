## Prerequisites

1. A minimum of 16GB of RAM + 16GB swap. 32GB+ RAM recommended with less swap required the more RAM you have.
2. A CPU that supports the AVX instruction set
3. wine 8.1 or newer. Follow the instructions on the [WineHQ website](https://wiki.winehq.org/Category:Distributions)
4. winetricks v20220411 or newer. Instructions are on the Winetricks [Github](https://github.com/Winetricks/winetricks/#installing)
5. dxvk-2.1 [or newer](https://github.com/doitsujin/dxvk)
6. vm.max_map_count set to at least 16777216
7. Hard open file descriptors limit set to at least 524288

**To check and set vm.max_map_count temporarily**
```
sysctl vm.max_map_count => To check the value
sudo sysctl -w vm.max_map_count=16777216 => To set it temporarily
```

**To set vm.max_map_count permanently**

_Distributions using systemd: Manjaro / Antergos / Arch / Arch-based (probably) / Ubuntu (and probably derivatives) / Fedora_

* Create a new file in `/etc/sysctl.d/`
* To name the file, the leading number is the priority of the file and the ending is `.conf`. For example, `"/etc/sysctl.d/20-max_map_count.conf"`.
* Add the following line to the file:
`vm.max_map_count = 16777216`

* To reload it, run `sudo sysctl --system`


_Distributions that use sysctl.conf_

* Append the same line to `/etc/sysctl.conf`
* To reload it, run `sudo sysctl -p`

**To set your system's hard open file descriptors limit**

_Distributions using systemd: Manjaro / Antergos / Arch / Arch-based (probably) / Ubuntu (and probably derivatives) / Fedora_

* Add the following line to /etc/systemd/system.conf: `DefaultLimitNOFILE=524288`

_Distributions that use /etc/security/limits.conf_

* Add the following line to /etc/security/limits.conf: `* hard nofile 524288`


## Installing

1. Install the necessary prerequisites
2. Create your wine prefix: `WINEPREFIX=~/path/you/want/to/Star-Citizen winecfg`
3. In the window that pops up, select **Windows 10** as Windows version and click OK
4. Run: `winetricks corefonts dxvk vcrun2017 win10`
5. Then you can run the RSI installer as normal.
6. You may need to create directory paths if the RSI installer is unable to do so:
```
mkdir -p "/path/to/prefix/drive_c/Program Files/Roberts Space Industries/StarCitizen/"{LIVE,PTU}
```
7. ONLY if you have black textures ingame, copy **d3dcompiler_47.dll** from the launcher directory to the games bin64/ directory, replacing the game's version.

If you have trouble installing recent Wine versions on a Debian-based distro due to missing faudio, see [this link](https://www.linuxuprising.com/2019/09/how-to-install-wine-staging-development.html).


## EAC Workaround

See the Manual Configuration instructions on our EAC wiki page [here](https://github.com/starcitizen-lug/knowledge-base/wiki/Tips-and-Tricks#easy-anti-cheat-workaround).
