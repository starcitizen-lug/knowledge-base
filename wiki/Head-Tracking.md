---
title: "Head Tracking"
nav_order: 7
---

# Head Tracking

## Hardware

### Hardware our Penguins have had success with
- Delanclip with Opentrack works very well and is our recommendation if you're buying new hardware.
- PS3 camera: Remove the IR filter. Some people place a visible light filter there instead to reduce noise.

### Use your Phone
- iPhone: Our Penguins tend to prefer the [Head Tracker app by John Yu](https://apps.apple.com/us/app/head-tracker/id1527710071). It works on iPhone X or later using the FaceID IR sensors and, therefore, works well in low light. It has a trial period to test it out. It costs $2 US.
- Android (Does not work on 14+): Our Penguins tend to like the [SmoothTrack app by John Goering](https://play.google.com/store/apps/details?id=com.epaga.smoothtrack&gl=US). It costs $10 US.
- Your phone can typically function as a webcam without any third party apps when connected to your computer. See the webcam section below.

### Webcam
- A tutorial for the the ArUco Paper Method is written in our Org's [Spectrum Forums](https://robertsspaceindustries.com/spectrum/community/LUG/forum/194647/thread/tutorial-opentrack-aruco-for-star-citizen-via-lutr). **NOTE:** Ignore the outdated Opentrack installation steps in that thread! See updated instructions below.
- Some Penguins have had success building [Opentrack with the ONNX Runtime](#building-opentrack-with-onnx-runtime) to add a neuralnet tracker that enables head tracking with any webcam.
- FOIP may be a bit finnicky and your camera may not appear in the list in-game, but has been known to work if you toggle it on and off a few times.

### Unsupported hardware
- Tobii does not support Linux. Its opentrack support uses the Windows only SDK.
- TrackIR 5 does not support Opentrack, nor does it work with Linuxtrack under Wine/Proton. We recommend Delanclip instead.


## Opentrack Configuration

{: .important }
> `GE Proton (Latest)` is the new umu Proton runner. The official Opentrack builds do not currently work with umu. We have reactivated the [opentrack-StarCitizen repo](https://github.com/Priton-CE/opentrack-StarCitizen) to provide this support. Our changes have been merged with the official [Opentrack Master branch](https://github.com/opentrack/opentrack/tree/master). Note that git builds of Opentrack may be less stable than our opentrack-StarCitizen until the next stable release of Opentrack.
> - For `system wine`, `wine-staging`, or `wine-GE-Proton8-x`, use an official Opentrack build version 2023.1.0 or later.
> - For any `GE-Proton` or `Proton` Runner, follow the [build instructions on our opentrack-StarCitizen repo](https://github.com/Priton-CE/opentrack-StarCitizen?tab=readme-ov-file#building-from-source). Alternatively, follow the [build instructions for Opentrack Master](https://github.com/opentrack/opentrack/wiki/Building-on-Linux) or use the [Opentrack-git AUR package](https://aur.archlinux.org/packages/opentrack-git). When running opentrack, include environment variable `PROTON_VERB="runinprefix"`
> - Some of our Penguins have reported issues with staging runners, so non-staging may be preferred.

After installing Opentrack according to the above note, use the following configuration:

1. Select `Wine` in the Output dropdown
2. Click the `Configure` button next to it
3. Under `Wine variant`, select one of the following:
    - Wine `Custom path to Wine executable`
      - Click `Browse Wine path` and select the `wine` executable inside the `bin` folder of your runner
      - Click `Browse Prefix` and select your Star Citizen prefix (e.g. `~/Games/star-citizen`)
    - Proton
      - Match your game's proton version
      - Pick `Steam Play` select number 1 (any number other than zero)
      - Pick `UMU enabled Launchers` and select your prefix
5. Confirm that the `ESYNC` and `FSYNC` settings match your settings
6. Next to `Protocol`, make sure `Both` is selected

Launch Star Citizen before clicking start in Opentrack.
Configure Star Citizen's head tracking options under `Comms, FOIP & Head Tracking`:
1. Set `Head Tracking - General - Source` to `TrackIR`
2. Set `Head Tracking - General - Toggle - Enabled` to `Yes`

{: .note }
> - May not work with Game Launchers in Flatpak
> - If compiling from source, make sure `SDK_WINE` is set
> - If compiling our custom Opentrack from source, make sure you are on the `wine-extended-proton` branch before building


## Building Opentrack with ONNX Runtime
If you provide ONNX Runtime libraries to Opentrack when building it, it will offer Neuralnet as input option. This will allow you to use any webcam as head tracking device.

Arch-based distros:
1. Install `onnxruntime` from the Arch repos.
2. Build and install [https://aur.archlinux.org/packages/opentrack](https://aur.archlinux.org/packages/opentrack) from the AUR. The PKGBUILD is already pre-configured to use the onnx runtime.

Other distros:
1. Install [`wine` development branch](https://wiki.winehq.org/Download).
2. Download and extract [ONNX Runtime](https://github.com/microsoft/onnxruntime/releases).
3. Follow [Opentrack's instructions](https://github.com/opentrack/opentrack/wiki/Building-on-Linux) with some extra steps when using `cmake` or `ccmake`.
    - Set variable `SDK_WINE`.
    - Set variable `ONNXRuntime_DIR` to absolute path to extracted ONNX Runtime folder.
    - If you're having trouble, some videos are provided by [bekopharm](https://linux.simpit.dev/systems/opentrack/)
4. Follow the configuration instructions [above](#opentrack-configuration).
5. Select `neuralnet tracker` as input.
   
{: .important }
> Do not remove ONNX Runtime after you are done. Opentrack won't have Neuralnet as input if you do remove it.

## Tobii Eye Tracker 5 VM Passthrough
Tobii Game Hub can send tracking data to Opentrack in a Windows VM by passing through the Tobii usb device from your linux host. Tracking can be forwarded to Opentrack on your host allowing you to use your Tobii Eye Tracker 5 with Star Citizen on Linux.

{: .important }
> - You will need spare CPU cores and RAM (4GB by default) to run the Windows VM at the same time as the game. Tested on a 3950X the CPU impact is negligable but you may experience issues on slower hardware.
> - Eye tracking with Opentrack can only be used for head movement and not for targeting.

### VM Setup
You will need a VM that supports passing through USB devices from the host. An existing VM can be used but you will need to modify the instructions below to support your virtualization software.  The instructions below will use a similar setup to [Winapps](https://github.com/winapps-org/winapps) using [dockur/windows](https://github.com/dockur/windows) to simplify the process of installing Windows with a QEMU backend.

Using Tiny11/Tiny10 for the Windows installation is reccomended as it has less CPU usage and lower disk space requirements.

#### How to set up a new Windows VM:
You can follow the same instructions provided by Winapps here - [Creating a Windows VM in Docker](https://github.com/winapps-org/winapps/blob/main/docs/docker.md#docker)

#### Add USB device passthrough for Tobii:
After your Windows is installed in your VM edit your docker compose.yml file to pass through the Tobii usb device by adding the following to the relevent sections:

```yaml
services:
  windows:
    environment:
      ARGUMENTS: "-device usb-host,vendorid=0x2104,productid=0x0313"
    devices:
      - /dev/bus/usb
    extra_hosts:
      - "host.docker.internal:host-gateway"

```
After making these changes run docker compose up to have them take effect for example:
```
docker compose --file ~/.config/winapps/compose.yaml up
```

Now you should be able to access your VM from the following URL:
`<http://localhost:8006>`

### Tobii Setup
1. Install the [Tobii Experience driver](https://gaming.tobii.com/getstarted/) on your Windows VM (Required)
2. Install both x86 and x64 [Microsoft Visual C++ Redistributable Packages](https://www.microsoft.com/en-my/download/details.aspx?id=40784) (Required for Tobii Game Hub to function)
3. Install [Tobii Game Hub](https://gaming.tobii.com/getstarted/?bundle=game-hub) (Required)
4. Install [opentrack](https://github.com/opentrack/opentrack/releases) on your Windows VM (Required)
5. Set your Windows VM display resolution to match your main monitor and enter fullscreen mode in novnc
6. Open the Tobii Experience application and run through setting up your Tobii eye tracker and monitor
7. Launch Tobii Game Hub and opentrack and verify that you can see the "running" status in Game Hub
8. Game Hub has many options to tweak how your head tracking is sent to opentrack. Adjusting these features and enabling options such as eye tracking should only be done once you have finished the full configuration below.

### Opentrack configuration (Windows)
1. [Follow the official Tobii documentation](https://help.tobii.com/hc/en-us/articles/28217654574865-How-to-do-Opentrack-setup-for-Tobii-Game-Hub-4-0) to set up opentrack correctly with Tobii Game Hub on your Windows VM
2. Verify that you are correctly seeing your head movement tracked in opentrack. Make sure to reset centre in Tobii Game Hub at least once. You might need to enable "Center at startup" in opentrack if you experience issues with head offset. 
3. Modify the opentrack Output setting to use "UDP over network" and enter the docker internal IP address of your host. If the IP address below does not work then do a nslookup on host.docker.internal from your Windows VM to find the correct IP address.
4. Click on Start to send tracking data to your Linux host via UDP.

    ![opentrack Windows config](https://github.com/user-attachments/assets/1d44f05e-72e0-4d5a-872a-3ec42b2fea7f){: style="display: block;max-width: 550px;" }

### Opentrack configuration (Linux Host)
1. [Follow the instructions above](#opentrack-configuration) to set up opentrack with support for wine
2. Set your Input to "UDP over network" and make sure the port matches your Windows VM opentrack configuration
3. Click on Start and you should see your tracking movements from your Windows VM mirrored
4. Update your Filter and Mapping configuration to match your Windows VM
5. You now should be able to launch Star Citizen and enable tracking

    ![opentrack Linux config](https://github.com/user-attachments/assets/95af9a1a-0833-4322-b4f0-c859a8cbdd55){: style="display: block;max-width: 600px;" }

### Automatically start tracking on Windows VM boot
You can configure windows to autostart Tobii Game Hub and opentrack so that you can just run docker compose up to enable tracking with one command.

1. Create a shortcut in your Windows startup directory to Tobii Game Hub by opening the run dialog (Start > Run) and typing "shell:startup" then create a new shortcut with the target "C:\Users\Docker\AppData\Local\TobiiGameHub\TobiiGameHub.exe"
2. Create a shortcut to opentrack with the target "C:\Program Files (x86)\opentrack\opentrack.exe"
3. Setup opentrack to start tracking on launch by adding an entry under Options > Game detection with the value of "opentrack.exe". Make sure to select the "Start profiles from game executable names in this list" checkbox

    ![opentrack Linux autostart](https://github.com/user-attachments/assets/07c4d95c-d12e-410a-b741-97f24c909a72){: style="display: block;max-width: 550px;" }
