## Recommended Distros
We strongly recommend choosing a distro that has up-to-date packages and a solid maintenance reputation.  

The following distributions make our 👍 list and generally work well with Star Citizen:
- Arch
- EndeavourOS (Arch-based)
- Fedora
- openSUSE Tumbleweed
- Debian Testing
- Ubuntu *(only the latest non-LTS release)*
- Gentoo

We do not recommend 👎 LTS distros. *LTS releases and out of date distros are likely to cause many headaches.* LTS ≠ stable. LTS just means old packages locked to a specific major version which only receive security updates. This is great for servers but terrible for gaming where new features and fixes are important. #LTSbadjustdontplskthx  

We do not recommend 👎 most gaming-focused distributions as many of our Penguins have had issues installing the required dependencies to make Star Citizen run. They generally have only an individual or a very small team backing them and, at least where Star Citizen is concerned, do not live up to the promise.  
- We especially suggest avoiding Pop!_OS and Drauger OS due to irresolvable compatibility issues

Other distributions we suggest avoiding 👎 due to frequent package incompatibilities, old dependencies, and update issues are: Manjaro, Ubuntu LTS, Mint (based on Ubuntu LTS), Debian Stable, and openSUSE Leap.

## Configuration differences required for NixOS
To set `vm.max_map_count` and `fs.file-max`, add the following to your NixOS config:

```nix
# ... your NixOS Config ...
boot.kernel.sysctl = {
  "vm.max_map_count" = 16777216;
  "fs.file-max" = 524288;
};
```
EAC configuration can be found [below](#manual-configuration).


## AMD FidelityFX Super Resolution (FSR) upscaling
In the Lutris `Runner options` tab, enable `AMD FidelityFX Super Resolution` or set the environment variable `WINE_FULLSCREEN_FSR=1`. Then, in the Star Citizen graphics settings, set the game to fullscreen and your desired resolution and it will be FSR scaled up. We recommend restarting the game after changing its resolution for better performance.


## Automatically Disable/Re-Enable Mouse Acceleration
Lutris can automatically toggle on/off a flat mouse acceleration profile with the following configuration.

Configure the game within Lutris and go to `System options`. Make sure `Show advanced options` is checked.  
Add the following to the `Pre-launch script` and `Post-exit script` fields.  
Alternatively, see [below](#lutris-pre-launch-and-post-exit-scripts) for a sample script file that incorporates this and other pre-launch tweaks.

**Gnome**

`/usr/bin/sh -c "gsettings set org.gnome.desktop.peripherals.mouse accel-profile flat"`

`/usr/bin/sh -c "gsettings set org.gnome.desktop.peripherals.mouse accel-profile default"`

**KDE**

`/usr/bin/sh -c 'kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" true'`

`/usr/bin/sh -c 'kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" false'`


## Easy Anti-Cheat Workaround
#### Automatic Configuration

_Using an Environment Variable_

* Set the following environment variable `Right click the game->Configure->System Options->Environment variables`:
  ```
  EOS_USE_ANTICHEATCLIENTNULL=1
  ```

_Using a GloriousEggroll runner_

GE runners since **Wine-GE-Proton7-41** include an EAC workaround by default. It will be enabled automatically for new installs. To enable it for existing installs:
* Set the following environment variable `Right click the game->Configure->System Options->Environment variables`:
  ```
  SteamGameId=starcitizen
  ```
* Add the following pre-launch command in Lutris `Right click the game->Configure->System Options->Pre-launch script`. Alternatively, see [below](#lutris-pre-launch-and-post-exit-scripts) for a script file that incorporates this.
  ```sh
  /usr/bin/sh -c 'if [ -d \"$WINEPREFIX/drive_c/users/$USER/AppData/Roaming/EasyAntiCheat\" ]; then rm -rf \"$WINEPREFIX/drive_c/users/$USER/AppData/Roaming/EasyAntiCheat\"; fi'
  ```

_/etc/hosts method:_

This applies the workaround globally at the system level by modifying /etc/hosts
* Launch the [LUG Helper](https://github.com/starcitizen-lug/lug-helper) and select `Deploy Easy Anti-cheat Workaround`
_json config method:_

If you prefer not to apply the workaround globally, a json file can be modified each time the game starts. Launcher updates/verifies will revert this change. Close and re-launch the game to re-apply it.
* In Lutris, navigate to `Right click the game->Configure->System Options->Pre-launch script`. Make sure `Show advanced options` is checked.
* Add the following. Alternatively, see [below](#lutris-pre-launch-and-post-exit-scripts) for a sample script file that incorporates this and other pre-launch tweaks.
  ```sh
  /usr/bin/sh -c "sed -i 's|\"productid\":.*|\"productid\": \"linux-eac-workaround\",|' \"$WINEPREFIX/drive_c/Program Files/Roberts Space Industries/StarCitizen/LIVE/EasyAntiCheat/Settings.json\""
  ```
* Enable `Wait for pre-launch script completion`
* Additional pre-launch script commands can be run using semicolons: `/usr/bin/sh -c "command1; command2; etc"`

#### Manual Configuration

_/etc/hosts method:_

* Add the following line to your `/etc/hosts` file:
`127.0.0.1 modules-cdn.eac-prod.on.epicgames.com #Star Citizen EAC workaround`
* Delete the following directory:
`$WINEPREFIX/drive_c/users/$USER/AppData/Roaming/EasyAntiCheat`

_json config method:_

* Edit `$WINEPREFIX/drive_c/Program Files/Roberts Space Industries/StarCitizen/LIVE/EasyAntiCheat/Settings.json` and modify the value of `productid`, `sandboxid`, `clientid`, or `deploymentid` to any invalid string, ie `linux-eac-workaround`.
* Delete the following directory:
`$WINEPREFIX/drive_c/users/$USER/AppData/Roaming/EasyAntiCheat`

_Configuration for NixOS users only:_

* Add `"127.0.0.1 modules-cdn.eac-prod.on.epicgames.com"` to [`networking.extraHosts`](https://search.nixos.org/options?channel=unstable&show=networking.extraHosts&from=0&size=50&sort=relevance&type=packages&query=networking.extraHosts)


## Lutris Pre-launch and Post-exit Scripts
Below are sample pre-launch and post-exit scripts that incorporate the mouse acceleration and EAC workarounds described above.  
To use them, create `sc-prelaunch.sh` and `sc-postexit.sh` in your wine prefix, uncomment the appropriate mouse acceleration lines based on your desktop environment, then configure Lutris to use the scripts:
- `Right click the game->Configure->System options` and set `Pre-launch script` to `/path/to/wine/prefix/sc-pre-launch.sh`
- `Right click the game->Configure->System options` and set `Post-exit script` to `/path/to/wine/prefix/sc-post-exit.sh`
- Enable `Wait for pre-launch script completion`

_sc-prelaunch.sh_
```bash
#!/bin/bash
############################################
## Lutris pre-launch script for Star Citizen
############################################

## Disable Mouse Acceleration
## GNOME
#gsettings set org.gnome.desktop.peripherals.mouse accel-profile flat

## KDE
#kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" true

## End Mouse Acceleration

## EAC Workaround
EACDIR="$WINEPREFIX/drive_c/users/$USER/AppData/Roaming/EasyAntiCheat"
GAMEDIR="$WINEPREFIX/drive_c/Program Files/Roberts Space Industries/StarCitizen"

## Remove EAC cache
## This is a necessary component of any EAC workaround method
if [ -d "$EACDIR" ]; then
    rm -rf "$EACDIR"
fi

## Mangle EAC settings.json
## This section is not needed if using a newer GE runner
for SCENV in LIVE PTU EPTU; do
  SETTINGS="$GAMEDIR/$SCENV/EasyAntiCheat/Settings.json"
  if [ -f "$SETTINGS" ]; then
    sed -i 's|\"productid\":.*|\"productid\": \"linux-eac-workaround\",|' "$SETTINGS"
  fi
done

## End EAC Workaround
```

_sc-postexit.sh_
```bash
#!/bin/bash
###########################################
## Lutris post-exit script for Star Citizen
###########################################

## Reset Mouse Acceleration
## Gnome
#gsettings set org.gnome.desktop.peripherals.mouse accel-profile default

## KDE
#kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" false

## End Mouse Acceleration
```


## Suggestions for a good gaming experience
https://robertsspaceindustries.com/spectrum/community/LUG/forum/149/thread/information-how-to-get-a-good-experience-with-star
> Join the org to access Spectrum links: https://robertsspaceindustries.com/orgs/LUG
