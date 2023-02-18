# Compatibility

In general, you can expect any hardware to work on linux but third-party software tied to the device can be an issue. In some cases, a VM may be required for configuring the device.

A collection of mappings used by our members can be found [here](https://github.com/starcitizen-lug/mappings).

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
