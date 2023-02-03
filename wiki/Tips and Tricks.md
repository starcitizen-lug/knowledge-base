## AMD FidelityFX Super Resolution (FSR) upscaling
In the Lutris `Runner options` tab, enable `AMD FidelityFX Super Resolution` or set the environment variable `WINE_FULLSCREEN_FSR=1`. Then, in the Star Citizen graphics settings, set the game to fullscreen and your desired resolution and it will be FSR scaled up. We recommend restarting the game after changing its resolution for better performance.

## Head tracking using Opentrack
At the moment, the simplest method to use Opentrack with Star Citizen is to install the Windows version of Opentrack within Lutris then select "Freetrack 2.0 enhanced" as the output. Save the following to a .yml file and use the Lutris option `Install from a local install script`

**Important**: Make sure `game_slug` matches your Star Citizen install in Lutris. `Right click the game->Configure` and look at the `Identifier` field.
```yml
name: "Opentrack for Star Citizen"
game_slug: star-citizen
version: Opentrack v2022.3.2
slug: star-citizen
description: "Opentrack for Star Citizen"
runner: wine
script:
  requires: star-citizen
  files:
    - opentrack-setup: https://github.com/opentrack/opentrack/releases/download/opentrack-2022.3.2/opentrack-2022.3.2-win32-setup.exe
  installer:
    - task:
        description: Installing Opentrack...
        executable: opentrack-setup
        name: wineexec
        prefix: $GAMEDIR

  game:
    exe: drive_c/Program Files (x86)/opentrack/opentrack.exe
    prefix: $GAMEDIR
```

## Automatically Disable/Re-Enable Mouse Acceleration
Lutris can automatically toggle on/off a flat mouse acceleration profile with the following configuration.

Configure the game within Lutris and go to `System options`. Make sure `Show advanced options` is checked.  
Add the following to the `Pre-launch script` and `Post-exit script` fields.  
Alternatively, see [below](https://github.com/starcitizen-lug/information-howtos/wiki/Tips-and-Tricks#lutris-pre-launch-and-post-exit-scripts) for a sample script file that incorporates this and other pre-launch tweaks.

**Gnome**

`/usr/bin/sh -c "gsettings set org.gnome.desktop.peripherals.mouse accel-profile flat"`

`/usr/bin/sh -c "gsettings set org.gnome.desktop.peripherals.mouse accel-profile default"`

**KDE**

`/usr/bin/sh -c 'kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" true'`

`/usr/bin/sh -c 'kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" false'`

## Rudder pedals
If your pedals aren't being recognized by Star Citizen, but work on Linux, it may be that it has been classified as something else than rudder pedals. This often happens because there are no buttons, and various OS functions assume it might be an accelerometer or similar.

There are two possible workarounds for this:

1) The following Python script creates a virtual device from the real device, adding a few more capabilities to make Star Citizen not discard it as an invalid device:
https://github.com/beniwtv/evdev-spoof-device

> Note: Consider making a pull request for your device (see quirks section), if there are quirks needed for your device to function.

2) Another solution is to create a Kernel udev rule to change the classification of your device. 

    * Create a file `/etc/udev/rules.d/90-pedals-workaround.rules`.
    * Add this to the file, changing your vendor and model IDs (can be found by using `lsusb`):

> ACTION=="add|change", KERNEL=="event[0-9]*", ENV{ID_VENDOR_ID}=="044f", ENV{ID_MODEL_ID}=="b679", ENV{ID_INPUT_ACCELEROMETER}="", ENV{ID_INPUT_JOYSTICK}="1", TAG+="uaccess"

> Also consider having the quirk added to systemd by following https://github.com/systemd/systemd/blob/main/hwdb.d/60-input-id.hwdb.

## Easy Anti-Cheat Workaround
**Automatic Configuration**

_/etc/hosts method:_

This applies the workaround globally at the system level by modifying /etc/hosts
* Launch the [LUG Helper](https://github.com/starcitizen-lug/lug-helper) and select `Deploy Easy Anti-cheat Workaround`

_json config method:_

If you prefer not to apply the workaround globally, a json file can be modified each time the game starts. Launcher updates/verifies will revert this change. Close and re-launch the game to re-apply it.
* In Lutris, navigate to `Right click the game->Configure->System Options->Pre-launch script`. Make sure `Show advanced options` is checked.
* Add the following. Alternatively, see [below](https://github.com/starcitizen-lug/information-howtos/wiki/Tips-and-Tricks#lutris-pre-launch-and-post-exit-scripts) for a sample script file that incorporates this and other pre-launch tweaks.
```sh
/usr/bin/sh -c "sed -i 's|\"productid\":.*|\"productid\": \"linux-eac-workaround\",|' \"$WINEPREFIX/drive_c/Program Files/Roberts Space Industries/StarCitizen/LIVE/EasyAntiCheat/Settings.json\""
```
* Enable `Wait for pre-launch script completion`
* Additional pre-launch script commands can be run using semicolons: `/usr/bin/sh -c "command1; command2; etc"`

**Manual Configuration**

_/etc/hosts method:_

* Add the following line to your `/etc/hosts` file:
`127.0.0.1 modules-cdn.eac-prod.on.epicgames.com #Star Citizen EAC workaround`
* Delete the following directory:
`$WINEPREFIX/drive_c/users/$USER/AppData/Roaming/EasyAntiCheat`

_json config method:_

* Edit `$WINEPREFIX/drive_c/Program Files/Roberts Space Industries/StarCitizen/LIVE/EasyAntiCheat/Settings.json` and modify the value of `productid`, `sandboxid`, `clientid`, or `deploymentid` to any invalid string, ie `linux-eac-workaround`.
* Delete the following directory:
`$WINEPREFIX/drive_c/users/$USER/AppData/Roaming/EasyAntiCheat`


## Lutris Pre-launch and Post-exit Scripts
Below are sample pre-launch and post-exit scripts that incorporate the mouse acceleration and EAC settings.json workaround described above.  
To use them, create `sc-pre-launch.sh` and `sc-post-exit.sh` in your wine prefix, uncomment the appropriate mouse acceleration lines based on your desktop environment, then configure Lutris to use the scripts:
- `Right click the game->Configure->System options` and set `Pre-launch script` to `/path/to/wine/prefix/sc-pre-launch.sh`
- `Right click the game->Configure->System options` and set `Post-exit script` to `/path/to/wine/prefix/sc-post-exit.sh`
- Enable `Wait for pre-launch script completion`

_sc-pre-launch.sh_
```bash
#!/bin/bash
############################################
## Lutris pre-launch script for Star Citizen
############################################

## Disable Mouse Acceleration 
## https://github.com/starcitizen-lug/information-howtos/wiki/Tips-and-Tricks#automatically-disablere-enable-mouse-acceleration

## GNOME
#gsettings set org.gnome.desktop.peripherals.mouse accel-profile flat

## KDE
#kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" true

## End Mouse Acceleration

## EAC Workaround
EACDIR="$WINEPREFIX/drive_c/users/$USER/AppData/Roaming/EasyAntiCheat"
GAMEDIR="$WINEPREFIX/drive_c/Program Files/Roberts Space Industries/StarCitizen"

## Remove EAC Cache
if [ -d "$EACDIR" ]; then
    rm -rf "$EACDIR"
fi

## Mangle EAC settings.json
for SCENV in LIVE PTU EPTU; do
  SETTINGS="$GAMEDIR/$SCENV/EasyAntiCheat/Settings.json"
  if [ -f "$SETTINGS" ]; then
    sed -i 's|\"productid\":.*|\"productid\": \"linux-eac-workaround\",|' "$SETTINGS"
  fi
done

## End EAC Workaround
```

_sc-post-exit.sh_
```bash
#!/bin/bash
###########################################
## Lutris post-exit script for Star Citizen
###########################################

## Reset Mouse Acceleration 
## https://github.com/starcitizen-lug/information-howtos/wiki/Tips-and-Tricks#automatically-disablere-enable-mouse-acceleration

## Gnome
#gsettings set org.gnome.desktop.peripherals.mouse accel-profile default

## KDE
#kwriteconfig5 --file "kcminputrc" --group "Mouse" --key "XLbInptAccelProfileFlat" false

## End Mouse Acceleration
```


## Suggestions for a good gaming experience
https://robertsspaceindustries.com/spectrum/community/LUG/forum/149/thread/information-how-to-get-a-good-experience-with-star
> Join the org to access Spectrum links: https://robertsspaceindustries.com/orgs/LUG
