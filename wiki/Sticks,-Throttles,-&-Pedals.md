---
title: "Sticks, Throttles, & Pedals"
description: "Peripheral compatibility and recommendations for Star Citizen on Linux, configuration tips, and troubleshooting."
nav_order: 6
md_message: "You are viewing raw source files... Go to https://wiki.starcitizen-lug.org/ to use the wiki!"
---

# Sticks, Throttles, & Pedals

## Compatibility
In general, you can expect any hardware to work on linux but third-party software tied to the device can be an issue. In some cases, a VM may be required for configuring the device.

**Troubleshooting**  
See the section [at the end of this page](#troubleshooting) for specific issues and workarounds.

## Recommendations

Virpil and VKB-sim are widely recommended for their build quality at their respective prices. It isn't recommended to go cheaper than these price ranges if you want something that will last.

Virpil has distribution centers in the EU and USA.  
[North America](https://virpil-controls.us.com/)  
[Europe](https://virpil-controls.eu/)  
[Russia](https://virpil-controls.by/)  

VKB has distribution centers in the EU, USA, and Australia. VKB also sells parts through their site as replacements or upgrades.  
[North America](https://www.vkbcontrollers.com/)  
[Europe](https://flightsimcontrols.com/)  
[Russia](https://shop.vkb-sim.pro/)  
[Australia, New Zealand](https://vkb-sim.com.au/)  
[India (AUS distribution)](https://vkb-sim.in/)  

## VKB Devices

{: .tip }
> Wine defaults to using HIDRAW to recognize common joysticks. To enable hidraw access to your VKB devices, create a rules file in `/etc/udev/rules.d` named `40-starcitizen-joystick-uaccess.rules`
```
# Set the "uaccess" tag for raw HID access for VKB Devices in wine
KERNEL=="hidraw*", ATTRS{idVendor}=="231d", ATTRS{idProduct}=="*", MODE="0660", TAG+="uaccess"
```


{: .important-title }
> After adding the udev rule
>
> Unplug and replug your device. The event joystick device may still show in the wine joystick control panel and will need to be disabled so that only the raw hid device is presented to the game. Follow the instructions in [Accessing Wine Game Controllers Settings](#accessing-wine-game-controllers-settings), select the device(s) that has `Sim (C) Alex Oz` in the name, and click the Disable button.

{: .important-title }
> Hidraw
>
> Hidraw is recommended for VKB devices running older firmware with a © symbol in the name, or consider upgrading your firmware
> You can check the device name using `lsusb` or `evdev-joystick --list`.

### VKB Gladiator

The Gladiator series can be calibrated without needing to use any special software.

They store their configuration on-board but the [configuration software](https://www.vkbcontrollers.com/pages/downloads) is only native to Windows. You can run the software in a virtual machine (VirtualBox, GNOME Boxes, etc) and pass the USB device to the windows environment to configure it that way.

### VKB Gunfighter

Requires a windows-only software for calibration and configuration. [Link](https://www.vkbcontrollers.com/pages/downloads)

## Virpil Devices

Requires a windows-only software for calibration and configuration. [Link; scroll down](https://support.virpil.com/en/support/solutions)

{: .tip }
> Wine defaults to using HIDRAW to recognize common joysticks. To enable hidraw access to your Virpil devices, create a rules file in `/etc/udev/rules.d` named `40-starcitizen-joystick-uaccess.rules` with the following content:
> ```
> # Set the "uaccess" tag for raw HID access for Virpil Devices in wine
> KERNEL=="hidraw*", ATTRS{idVendor}=="3344", ATTRS{idProduct}=="*", MODE="0660", TAG+="uaccess"
> ```

{: .important-title }
> After adding the udev rule
>
> Unplug and replug your device. The event joystick device may still show in the wine joystick control panel and will need to be disabled so that only the raw hid device is presented to the game. Follow the instructions in [Accessing Wine Game Controllers Settings](#accessing-wine-game-controllers-settings), select the non-hidraw device(s), and click the Disable button.

## ThrustMaster Devices

{: .tip }
> Wine defaults to using HIDRAW to recognize common joysticks. To enable hidraw access to your ThrustMaster devices, create a rules file in `/etc/udev/rules.d` named `40-starcitizen-joystick-uaccess.rules` with the following content:
> ```
> # Set the "uaccess" tag for raw HID access for ThrustMaster Devices in wine
> KERNEL=="hidraw*", ATTRS{idVendor}=="044f", ATTRS{idProduct}=="*", MODE="0660", TAG+="uaccess"
> ```

{: .important-title }
> After adding the udev rule
>
> Unplug and replug your device. The event joystick device may still show in the wine joystick control panel and will need to be disabled so that only the raw hid device is presented to the game. Follow the instructions in [Accessing Wine Game Controllers Settings](#accessing-wine-game-controllers-settings), select your device(s), and click the Disable button.

### Thrustmaster T-16000

**Potentiometer Failure**  
The yaw potentiometer on these sticks tends to fail after a time. It may be possible to prevent or fix the issue, otherwise a new potentiometer can be soldered on.
- Disassemble the grip and trim off some plastic to try to [fix or prevent the problem](https://www.reddit.com/r/hotas/comments/9h5va3/t16000_yaw_fixed/)
- Disassemble the potentiometer to try to [clean and repair it](https://www.reddit.com/r/hotas/comments/7ec712/comment/dq58sy8/?context=3)
- A bit of soldering to [replace the potentiometer](https://www.reddit.com/r/hotas/comments/cronns/comment/ex8oo4b/?context=3)

- Thrustmaster T16000 sticks may not appear in the Game Controllers list unless DLL overrides for dinput and xinput are added:
    - Use the LUG Helper's Maintenance menu `Open Wine prefix configuration` option
    - In the Wine configuration window, select the `Libraries` tab.
    - Use the `New override for library` dropdown to add overrides for `dinput` and `xinput`.
    - If there is more than one `xinput` entry, add them all.

### Thrustmaster SOL-R

**Manual Calibration**  
1. Start with base unplugged.
2.  Push the upper trigger and press the left button (35) on grip then plug to USB port into the base and calibration will start. The ring LED around thumb-stick will blink slowly when calibration process is active.
3. Let the thumb-stick and the twist rest to center position and push the scroll-wheel below the thumb stick to set the center position, the LED around thumb-stick will blink faster.
4. Reach the maximum & minimum of both thumb-stick axis without applying too much force.
5. Reach the maximum position on left and right side of twist without applying too much force on both end.
6. Push again the scroll-wheel to validate the calibration, LED stop to blink to indicate the calibration process is complete. To exit the calibration mode unplug /replug the USB cable.

Change LEDs with a simple python script

[https://github.com/gort818/solr-led/blob/main/solr-led.py](https://github.com/gort818/solr-led/blob/main/solr-led.py)


## Other Devices

{: .tip }
> Wine defaults to using HIDRAW to recognize common joysticks. Follow the instructions below to obtain device info and enable HIDRAW.

### Find Device Info
Use `udevadm` to retrieve the Vendor ID, Model Name, and Model ID that the device reports to the system.
```bash
udevadm info -n /dev/input/by-id/usb-your-joystick-name | grep -E 'ID_VENDOR_ID|ID_MODEL_ID|ID_MODEL'
```
Example:
```bash
$ udevadm info -n /dev/input/by-id/usb-VKB-Sim_©_Alex_Oz_2021_VKBsim_Space_Gunfighter-event-joystick | grep -E 'ID_VENDOR_ID|ID_MODEL_ID|ID_MODEL'
E: ID_VENDOR_ID=231d
E: ID_MODEL=VKBsim_Space_Gunfighter
E: ID_MODEL_ENC=\x20VKBsim\x20Space\x20Gunfighter\x20
E: ID_MODEL_ID=0126
```

### Enable HIDRAW

- Create a rules file in `/etc/udev/rules.d` named `40-starcitizen-joystick-uaccess.rules` with the following content. Replace <ID_VENDOR_ID> with the Vendor ID retrieved in the step above. For working examples, see the VKB, Virpil, or Thrustmaster sections above.
 ```
 # Set the "uaccess" tag for raw HID access for input devices in wine.
 KERNEL=="hidraw*", ATTRS{idVendor}=="<ID_VENDOR_ID>", ATTRS{idProduct}=="*", MODE="0660", TAG+="uaccess"
 ```

{: .important-title }
> After adding the udev rule
> 
> Unplug and replug your device. The event joystick device may still show in the wine joystick control panel and will need to be disabled so that only the raw hid device is presented to the game. Follow the instructions in [Accessing Wine Game Controllers Settings](#accessing-wine-game-controllers-settings), select the device(s) that **do not** match the results of the [Find Device Info](#find-device-info) step above, and click the Disable button.

## Mappings

A collection of mappings contributed by our community can be found [here](https://github.com/starcitizen-lug/mappings).  
Mappings for Saitek / Logitech x56 HOTAS are maintained individually by @PaladinTitus [here](https://github.com/PaladinTitus/SC_X56).  

The third party tool, [input-remapper](https://github.com/sezanzeb/input-remapper), can be used to change the behavior of input devices. Note that, while some of our Penguins have had success using this tool, we have not fully vetted its functionality or safety. Some basic profile examples contributed by our community can be found [here](https://github.com/starcitizen-lug/mappings/tree/main/input-remapper).


## Evdev Deadzones

{: .warning }
> 
> This section does not apply if your controllers are connected as HIDRAW devices.

For non-hidraw devices, evdev may add extra deadzones to your controller on top of those configured by the device's firmware. Throttles may experience a "hitch" in the center of their axis. You can remove these deadzones with a udev rule.

1. Install `evdev-joystick`. This utility is provided by different packages depending on your distribution.  
See the list below for your distribution:
    - Arch - `linuxconsole`
    - Debian/Ubuntu - `joystick`
    - Fedora - `linuxconsoletools`

2. Create a udev rules file in  
`/etc/udev/rules.d/` and replace [your device info](#find-device-info) in the following template:

```
# Custom Joystick Udev Rules

# Sample
ACTION=="add", SUBSYSTEM=="input", KERNEL=="event*", \
  ENV{ID_VENDOR_ID}=="<Vendor ID>", ENV{ID_MODEL_ID}=="<Model ID>", \
  RUN+="/usr/bin/evdev-joystick --e %E{DEVNAME} --d 0" 
```

**Example rules**  
`/etc/udev/rules.d/99-evdev-joystick.rules`
```
# Custom Joystick Udev Rules

# VKB SEM
ACTION=="add", SUBSYSTEM=="input", KERNEL=="event*", \
  ENV{ID_VENDOR_ID}=="231d", ENV{ID_MODEL_ID}=="2204", \
  RUN+="/usr/bin/evdev-joystick --e %E{DEVNAME} --d 0" 

# VKB Gunfighter L
ACTION=="add", SUBSYSTEM=="input", KERNEL=="event*", \
  ENV{ID_VENDOR_ID}=="231d", ENV{ID_MODEL_ID}=="0127", \
  RUN+="/usr/bin/evdev-joystick --e %E{DEVNAME} --d 0" 

# VKB Gunfighter R
ACTION=="add", SUBSYSTEM=="input", KERNEL=="event*", \
  ENV{ID_VENDOR_ID}=="231d", ENV{ID_MODEL_ID}=="0126", \
  RUN+="/usr/bin/evdev-joystick --e %E{DEVNAME} --d 0" 

# Virpil Rudder Pedals
ACTION=="add", SUBSYSTEM=="input", KERNEL=="event*", \
  ENV{ID_VENDOR_ID}=="3344", ENV{ID_MODEL_ID}=="01f8", \
  RUN+="/usr/bin/evdev-joystick --e %E{DEVNAME} --d 0" 
```

## Troubleshooting

### Accessing Wine Game Controllers Settings
- Run the [LUG Helper](/Tips-and-Tricks#how-to-run-the-lug-helper), select the `Maintenance and Troubleshooting` menu, then choose `Open Wine controller configuration`.
- For alternative installs using third party launchers, refer to that launcher's help and/or menu options, or manually run `WINEPREFIX=/path/to/your/prefix wine control joy.cpl`

### Some of your joysticks disappear / aren't recognized in the game
- You may need to enable HIDRAW access. See [VKB](#vkb-devices), [Virpil](#virpil-devices), or [Thrustmaster](#thrustmaster-devices) sections above for instructions
- Try setting your joysticks to "dinput" instead of "xinput" in Wine control panel
    - Follow the [Accessing Wine Game Controllers Settings](#accessing-wine-game-controllers-settings) instructions above.
    - If your joysticks are showing up as "Connected(xinput)", select them and click "Override" to set them to dinput.

### Some of your joystick axis aren't recognized / don't map
- Check that the game has not set the deadzone for this axis to 100%

### Rudder pedals not recognized
If your pedals aren't being recognized by Star Citizen but work on Linux, it may be that it has been classified as something else than rudder pedals. This often happens because there are no buttons, and various OS functions assume it might be an accelerometer or similar.

There are two possible workarounds for this:

- The following Python script creates a virtual device from the real device, adding a few more capabilities to make Star Citizen not discard it as an invalid device:
https://github.com/beniwtv/evdev-spoof-device

- Another solution is to create a Kernel udev rule to change the classification of your device. 

    - Create a file `/etc/udev/rules.d/90-pedals-workaround.rules` and plug [your device info](#find-device-info) into the following template:
      ```
      ACTION=="add|change", KERNEL=="event[0-9]*", ENV{ID_VENDOR_ID}=="<Your Vendor ID>", ENV{ID_MODEL_ID}=="<Your Model ID>", ENV{ID_INPUT_ACCELEROMETER}="", ENV{ID_INPUT_JOYSTICK}="1", TAG+="uaccess"
      ```
