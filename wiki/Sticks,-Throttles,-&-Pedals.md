# Compatibility

In general, you can expect any hardware to work on linux but third-party software tied to the device can be an issue. In some cases, a VM may be required for configuring the device.

**Troubleshooting**: See the section [at the end of this page](#troubleshooting) for specific issues and workarounds.

## Recommendations

Virpil and VKB-sim are widely recommended for their build quality at their respective prices. It isn't recommended to go cheaper than these price ranges if you want something that will last.

Virpil has distribution centers in the EU and USA.  
[North America](https://virpil-controls.us.com/)  
[Europe](https://virpil-controls.eu/)  
[Russia](https://virpil.by/)  

VKB has distribution centers in the EU, USA, and Australia. VKB also sells parts through their site as replacements or upgrades.  
[North America](https://www.vkbcontrollers.com/)  
[Europe](https://flightsimcontrols.com/)  
[Russia](https://shop.vkb-sim.pro/)  
[Australia, New Zealand](https://vkb-sim.com.au/)  
[India (AUS distribution)](https://vkb-sim.in/)  

## VKB Gladiator

The Gladiator series can be calibrated without needing to use any special software.

They store their configuration on-board but the [configuration software](https://www.vkbcontrollers.com/pages/downloads) is only native to Windows. You can run the software in a virtual machine (VirtualBox, GNOME Boxes, etc) and pass the USB device to the windows environment to configure it that way.

## VKB Gunfighter

Requires a windows-only software for calibration and configuration. [Link](https://www.vkbcontrollers.com/pages/downloads)

## Virpil 
    
Requires a windows-only software for calibration and configuration. [Link; scroll down](https://support.virpil.com/en/support/solutions)

## Configuration Tips

### Mappings

A collection of mappings used by our members can be found [here](https://github.com/starcitizen-lug/mappings).

### Evdev Deadzones

On Linux, evdev adds deadzones to every axis for each controller you plug into your system.  This is good for inexpensive controllers that don't have any form of internal calibration or programming.  However, with higher end programmable sticks like those from VKB and Virpil, evdev's deadzone adds to the programmed deadzone for those devices.  This can also impact throttle devices, where you can get a "hitch" at 50% throttle when it passes through the middle of the axis.

To eliminate this problem, you want to create a udev rule that removes the evdev deadzone from your devices when they're plugged in.

First, install `evdev-joystick`. This utility is provided by different packages depending on your distribution.  
See the list below for your distribution:
* Arch - `linuxconsole`
* Debian/Ubuntu - `joystick`
* Fedora - `linuxconsoletools`

Then, you will need the Vendor ID, Model Name, and Model ID that the device reports to the system.  
You can get this information with `udevadm`

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

With this information for each device you have that you want to eliminate the evdev deadzone for, create a udev rules file in  
`/etc/udev/rules.d/` and plug in the information into the following template:

```
# Custom Joystick Udev Rules

# Sample
ACTION=="add", SUBSYSTEM=="input", KERNEL=="event*", \
  ENV{ID_VENDOR_ID}=="<Vendor ID>", ENV{ID_MODEL_ID}=="<Model ID>", \
  RUN+="/usr/bin/evdev-joystick --e %E{DEVNAME} --d 0" 
```

This will keep things very specific to just the devices you want to change, and not impact any other devices you use.


Here is an example rules file for 3 VKB devices and one Virpil device:  
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

# Troubleshooting

### Rudder pedals
If your pedals aren't being recognized by Star Citizen but work on Linux, it may be that it has been classified as something else than rudder pedals. This often happens because there are no buttons, and various OS functions assume it might be an accelerometer or similar.

There are two possible workarounds for this:

1) The following Python script creates a virtual device from the real device, adding a few more capabilities to make Star Citizen not discard it as an invalid device:
https://github.com/beniwtv/evdev-spoof-device

> Note: Consider making a pull request for your device (see quirks section), if there are quirks needed for your device to function.

2) Another solution is to create a Kernel udev rule to change the classification of your device. 

    * Create a file `/etc/udev/rules.d/90-pedals-workaround.rules`.
    * Add this to the file, changing your vendor and model IDs (can be found by using `lsusb`):

> ACTION=="add|change", KERNEL=="event[0-9]*", ENV{ID_VENDOR_ID}=="044f", ENV{ID_MODEL_ID}=="b679", ENV{ID_INPUT_ACCELEROMETER}="", ENV{ID_INPUT_JOYSTICK}="1", TAG+="uaccess"

> Also consider having the quirk added to systemd by following https://github.com/systemd/systemd/blob/main/hwdb.d/60-input-id.hwdb.

### Thrustmaster T-16000

The yaw potentiometer on these sticks tends to fail after a time. It may be possible to prevent or fix the issue, otherwise a new potentiometer can be soldered on.
- Disassemble the grip and trim off some plastic to try to [fix or prevent the problem](https://www.reddit.com/r/hotas/comments/9h5va3/t16000_yaw_fixed/)
- Disassemble the potentiometer to try to [clean and repair it](https://www.reddit.com/r/hotas/comments/7ec712/comment/dq58sy8/?context=3)
- A bit of soldering to [replace the potentiometer](https://www.reddit.com/r/hotas/comments/cronns/comment/ex8oo4b/?context=3)
