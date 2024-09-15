## Prerequisites
New to Linux? See our [Recommended Distributions](Tips-and-Tricks#recommended-distros) for a list of the distros most compatible with Star Citizen.

1. Install wine following the [instructions for your distro](https://gitlab.winehq.org/wine/wine/-/wikis/Download). See the [WineHQ Main Page](https://www.winehq.org/) for current versions. **If your distro provides an up to date version of wine** (ie. Arch), you may install from its repos instead. 
2. Install winetricks 20240105-next or newer. Instructions are on the Winetricks [Github](https://github.com/Winetricks/winetricks/#installing)
3. Install dxvk-2.4 [or newer](https://github.com/doitsujin/dxvk) and configure it for your distribution
4. Set `vm.max_map_count` on your system to at least `16777216`
5. Set the Hard open file descriptors limit on your system to at least `524288`

**To check and set vm.max_map_count temporarily**
```
sysctl vm.max_map_count => To check the value
sudo sysctl -w vm.max_map_count=16777216 => To set it temporarily
```

**To set vm.max_map_count permanently**

_Distributions using sysctl.d: Manjaro / Antergos / Arch / Arch-based (probably) / Ubuntu (and probably derivatives) / Fedora_

* Create a new drop-in config file: `/etc/sysctl.d/99-starcitizen-max_map_count.conf`
* Add the following line to the file: `vm.max_map_count = 16777216`
* To reload it, run `sudo sysctl --system`


_Distributions that use sysctl.conf_

* Append the same line to `/etc/sysctl.conf`
* To reload it, run `sudo sysctl --system`

**To set your system's hard open file descriptors limit**

_Distributions using systemd: Manjaro / Antergos / Arch / Arch-based (probably) / Ubuntu (and probably derivatives) / Fedora_

* Create a new drop-in config file: `/etc/systemd/systemd.conf.d/99-starcitizen-filelimit.conf`
* Add the following line to the file: `DefaultLimitNOFILE=524288`
* To reload it, run `sudo systemctl daemon-reexec`

_Distributions that use /etc/security/limits.conf_

* Add the following line to /etc/security/limits.conf: `* hard nofile 524288`


## Installing

1. Install and configure the necessary prerequisites
2. Create your wine prefix: `WINEPREFIX=~/path/you/want/to/starcitizen winecfg`
3. In the window that pops up, select **Windows 10** as Windows version and click OK
4. Run: `winetricks corefonts dxvk vcrun2017 win10`
5. Download and run the RSI installer
6. You may need to create directory paths if the RSI installer is unable to do so:
```
mkdir -p "/path/to/prefix/drive_c/Program Files/Roberts Space Industries/StarCitizen/"{LIVE,PTU,EPTU,TECH-PREVIEW}
```
7. ONLY if you have black textures ingame, copy **d3dcompiler_47.dll** from the launcher directory to the games bin64/ directory, replacing the game's version.
8. To use a custom wine runner, start the game/installer with `WINE=/path/to/runner/bin/wine`

If you have trouble installing recent Wine versions on a Debian-based distro due to missing faudio, see [this link](https://www.linuxuprising.com/2019/09/how-to-install-wine-staging-development.html).


## EAC Workaround

See the Manual Configuration instructions on our EAC wiki page [here](https://github.com/starcitizen-lug/knowledge-base/wiki/Tips-and-Tricks#easy-anti-cheat-workaround).
