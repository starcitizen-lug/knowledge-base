---
title: "Quick-Start Guide"
description: "Simple steps to install Star Citizen on Linux!"
nav_order: 2
---
# Quick-Start Guide

{: .tip-title }
> New to Linux?
>
> See our [Recommended Distributions](Tips-and-Tricks#recommended-distros) for a list of the distros most compatible with Star Citizen.

## Prerequisites

1. Install `cabextract` and `unzip` from your distro's repos; these are needed by Winetricks. Alternatively, install winetricks **20250102** or newer from your distro's repos. Links, if needed, are on the winetricks [github](https://github.com/Winetricks/winetricks#installing)
2. Select an install location where you have space for the entire game, approximately 140GB
    - Must be a linux-formatted SSD
    - We do not recommend an HDD or NTFS format

{: .tip }
> If using an immutable distro that is unable to satisfy the Prerequisites above, we recommend the [flatpak installation](Alternative-Installations#flatpak-installation).
>
> For NixOS, see instructions [here](/Alternative-Installations#nixos-installation).  
> For the Steam Deck, see instructions [here](/Alternative-Installations#steam-deck-installation)

## Installation Steps

1. Download our [LUG Helper](https://github.com/starcitizen-lug/lug-helper/releases/latest) (Select the `.tar.gz`. Distro packages are listed [here](https://github.com/starcitizen-lug/lug-helper#installation))
2. [Launch](Tips-and-Tricks#how-to-run-the-lug-helper) the LUG Helper and select `Install Star Citizen`
3. Allow the Preflight Check to fix any issues it finds before proceeding!
4. You may instruct the Helper to install the Wine prefix (this contains the game) to any linux-formatted partition.
5. After the install completes, run the RSI Launcher, log in, and click Install to finish installing the game. **Do not** change the default install location `C:\Program Files\Roberts Space Industries`!
6. Launch the game. See you in the 'verse!

## After Installation

{: .important }
> - For non-US keyboards, set your [keyboard layout](Troubleshooting/unexpected-behavior#non-us-keyboard-keys-not-working) to resolve issues with game console and accept/reject buttons
> - Wayland users: See [required workarounds](Troubleshooting/unexpected-behavior#mousecursor-warp-issues-and-view-snapping-in-interaction-mode) to resolve mouse cursor and view snapping issues.
> - Nvidia users: See [troubleshooting guide](Troubleshooting/nvidia#severe-frame-drops) to resolve severe frame drop issues.
> - Check our [latest news](/#news) for necessary workarounds, Nvidia gpu driver problems, and other important issues.

{: .note-title }
> Questions or Problems?
>
> - Check our [Troubleshooting Guide](Troubleshooting) or ask for help in one of our [social channels](/#join-us)!
