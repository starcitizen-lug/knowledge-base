## Head Tracking Hardware

#### Hardware our Penguins have had success with
- Delanclip with Opentrack works very well and is our recommendation if you're buying new hardware.
- PS3 camera: Remove the IR filter. Some people place a visible light filter there instead to reduce noise.

#### Use your Phone
- iPhone: Our Penguins tend to prefer the [Head Tracker app by John Yu](https://apps.apple.com/us/app/head-tracker/id1527710071). It works on iPhone X or later using the FaceID IR sensors and, therefore, works well in low light. It has a trial period to test it out. It costs $2 US.
- Android: Our Penguins tend to like the [SmoothTrack app by John Goering](https://play.google.com/store/apps/details?id=com.epaga.smoothtrack&gl=US). It costs $10 US.

#### Webcam
- You can build [Opentrack with the ONNX Runtime](#building-opentrack-with-onnx-runtime) to add a neuralnet tracker that enables head tracking with any webcam.
- A tutorial for the the ArUco Paper Method is written in our Org's [Spectrum Forums](https://robertsspaceindustries.com/spectrum/community/LUG/forum/194647/thread/tutorial-opentrack-aruco-for-star-citizen-via-lutr). (Note: Ignore the outdated Opentrack installation steps in that thread)

#### Unsupported hardware
- Tobii does not support Linux. Its opentrack support uses the Windows only SDK.
- TrackIR support is complicated. Linuxtrack may support it but not under wine/proton. We recommend Delanclip instead.


## Opentrack Configuration
Opentrack versions 2023.1.0 and later contain the fixes needed to work with Star Citizen. After installing it, use the following configuration:

1. Select `Wine` in the Output dropdown
2. Click the `Configure` button next to it
3. Under `Wine variant`, select the `Wine` radio button and then choose the Wine version or Lutris Runner you're using with Star Citizen
4. Click `Browse Prefix` and select your Star Citizen Wine prefix (Lutris Default: ~/Games/star-citizen)
5. Next to `Protocol`, make sure `Both` is selected

Launch Star Citizen and configure its head tracking options under `Comms, FOIP & Head Tracking`
1. Set `Head Tracking - General - Source` to `TrackIR`
2. Set `Head Tracking - General - Toggle - Enabled` to `Yes`

*Notes:*  
*May not work with Flatpak Lutris*  
*If compiling from source, make sure `SDK_WINE` is set*

## Building Opentrack with ONNX Runtime
If you provide ONNX Runtime libraries to Opentrack when building it, it will offer Neuralnet as input option. This will allow you to use any webcam as head tracking device.

1. Install [`wine` development branch](https://wiki.winehq.org/Download).
2. Download and extract [ONNX Runtime](https://github.com/microsoft/onnxruntime/releases).
3. Install [Opentrack](https://github.com/opentrack/opentrack/wiki/Building-on-Linux) with some extra steps when using `cmake` or `ccmake`.
    - Set variable `SDK_WINE`.
    - Set variable `ONNXRuntime_DIR` to absolute path to extracted ONNX Runtime folder.
4. Follow [above instructions](#head-tracking-using-opentrack).
5. Select `neuralnet tracker` as input.

*Note:*  
*Do not remove ONNX Runtime after you are done. Opentrack won't have Neuralnet as input if you do remove it.*
