## Prerequisites

1. A minimum of 16GB of RAM
2. A CPU that supports the AVX instruction set
3. wine-staging (or just the dependencies) installed on your system. Follow this guide: https://www.gloriouseggroll.tv/how-to-get-out-of-wine-dependency-hell/
4. winetricks v20210825 or newer: https://github.com/Winetricks/winetricks/#installing
5. vm.max_map_count set to at least 16777216
6. Hard open file descriptors limit set to at least 524288

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

**To apply the EAC Workaround**

Add the following line to your /etc/hosts file:

`127.0.0.1 modules-cdn.eac-prod.on.epicgames.com #Star Citizen EAC workaround`

## Installing

* Install vanilla Wine 7.14+ or a custom Runner **(As of 3.13 we recommend a [runner built for Star Citizen](https://github.com/starcitizen-lug/information-howtos/wiki/Wine-Builds-for-Star-Citizen))**
* Create your wine prefix: `WINEPREFIX=~/path/you/want/to/Star-Citizen winecfg`

* In the window that pops up, select **Windows 10** as Windows version and click OK
* Install winetricks from either your distribution or https://github.com/Winetricks/winetricks (if your winetricks doesn't have at least DXVK 1.6)
* Run: `winetricks corefonts dxvk vcrun2017 win10`

* Then you can run the RSI installer as normal.
* You may need to create directory paths if the RSI installer is unable to do so:
```
mkdir -p "/path/to/prefix/drive_c/Program Files/Roberts Space Industries/StarCitizen/"{LIVE,PTU}
```
* ONLY if you have black textures ingame, copy **d3dcompiler_47.dll** from the launcher directory to the games bin64/ directory, replacing the game's version.

If you have trouble installing recent Wine versions on a Debian-based distro due to missing faudio, see:

https://www.linuxuprising.com/2019/09/how-to-install-wine-staging-development.html

## EAC Workaround

Hosts method:
* Add the following line to your `/etc/hosts` file:
`127.0.0.1 modules-cdn.eac-prod.on.epicgames.com #Star Citizen EAC workaround`

json method:
* Edit `$WINEPREFIX/drive_c/Program Files/Roberts Space Industries/StarCitizen/LIVE/EasyAntiCheat/Settings.json` and modify the value of `productid`, `sandboxid`, `clientid`, or `deploymentid` to any invalid string, ie `linux-user`.
