## Head Tracking Hardware

#### Hardware our Penguins have had success with
- Delanclip with Opentrack works very well and is our recommendation if you're buying new hardware.
- PS3 camera: Remove the IR filter. Some people place a visible light filter there instead to reduce noise.

#### Use your Phone
- iPhone: Our Penguins tend to prefer the [Head Tracker app by John Yu](https://apps.apple.com/us/app/head-tracker/id1527710071). It works on iPhone X or later using the FaceID IR sensors and, therefore, works well in low light. It has a trial period to test it out. It costs $2 US.
- Android: Our Penguins tend to like the [SmoothTrack app by John Goering](https://play.google.com/store/apps/details?id=com.epaga.smoothtrack&gl=US). It costs $10 US.

#### Webcam
- A tutorial for the the ArUco Paper Method is written in our Org's [Spectrum Forums](https://robertsspaceindustries.com/spectrum/community/LUG/forum/194647/thread/tutorial-opentrack-aruco-for-star-citizen-via-lutr). **NOTE:** Ignore the outdated Opentrack installation steps in that thread! See updated instructions below.
- Some Penguins have had success building [Opentrack with the ONNX Runtime](#building-opentrack-with-onnx-runtime) to add a neuralnet tracker that enables head tracking with any webcam.

#### Unsupported hardware
- Tobii does not support Linux. Its opentrack support uses the Windows only SDK.
- TrackIR 5 does not support Opentrack, nor does it work with Linuxtrack under Wine/Proton. We recommend Delanclip instead.


## Opentrack Configuration
> [!important]
> `GE Proton (Latest)` is the new umu Proton runner. The official Opentrack builds do not currently work with umu. We have reactivated the [opentrack-StarCitizen repo](https://github.com/Priton-CE/opentrack-StarCitizen) to provide this support. Our changes have been merged with the official [Opentrack Master branch](https://github.com/opentrack/opentrack/tree/master). Note that git builds of Opentrack may be less stable than our opentrack-StarCitizen until the next stable release of Opentrack.
> - For `system wine`, `wine-staging`, or `wine-GE-Proton8-x`, use an official Opentrack build version 2023.1.0 or later.
> - For any `GE-Proton` or `Proton` Runner, follow the [build instructions on our opentrack-StarCitizen repo](https://github.com/Priton-CE/opentrack-StarCitizen?tab=readme-ov-file#building-from-source). Alternatively, follow the [build instructions for Opentrack Master](https://github.com/opentrack/opentrack/wiki/Building-on-Linux) or use the [Opentrack-git AUR package](https://aur.archlinux.org/packages/opentrack-git).

After installing Opentrack according to the above note, use the following configuration:

1. Select `Wine` in the Output dropdown
2. Click the `Configure` button next to it
3. Under `Wine variant`, select one of the following:
    1. `Wine` if using a Wine Runner as mentioned in the note above. Then, choose the Wine version or Lutris Wine Runner you're using with Star Citizen.
    2. `Proton` and then `UMU enabled Launchers` if using a Proton Runner with our custom opentrack-StarCitizen. Then, choose the Proton version you have selected in Lutris.
4. Click `Browse Prefix` and select your Star Citizen prefix (Lutris Default: `~/Games/star-citizen`)
5. Confirm that the `ESYNC` and `FSYNC` settings match your settings in Lutris.
6. Next to `Protocol`, make sure `Both` is selected

Launch Star Citizen before clicking start in Opentrack.  
Configure Star Citizen's head tracking options under `Comms, FOIP & Head Tracking`:
1. Set `Head Tracking - General - Source` to `TrackIR`
2. Set `Head Tracking - General - Toggle - Enabled` to `Yes`  

> [!note]
> - May not work with Flatpak Lutris
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
> [!note]
> Do not remove ONNX Runtime after you are done. Opentrack won't have Neuralnet as input if you do remove it.
