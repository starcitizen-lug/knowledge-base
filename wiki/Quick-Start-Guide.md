---
title: "Quick-Start Guide"
description: "Simple steps to install Star Citizen on Linux!"
nav_order: 2
md_message: "You are viewing raw source files... Go to https://wiki.starcitizen-lug.org/ to use the wiki!"
---
# Quick-Start Guide

{: .tip-title }
> New to Linux?
>
> See our [Recommended Distributions](Tips-and-Tricks#recommended-distros) for a list of the distros most compatible with Star Citizen.

## Prerequisites

1. Install `cabextract` and `unzip` using your package manager; these are needed by Winetricks. Alternatively, install winetricks **20250102** or newer from your package manager. Links, if needed, are on the winetricks [github](https://github.com/Winetricks/winetricks#installing)
2. Decide on an install location where you have space for the entire game, approximately 140GB
    - Must be a linux-formatted SSD
    - We do not recommend an HDD or NTFS format

{: .tip }
> If your distro does not satisfy the prerequisites, we recommend the [flatpak installation](Alternative-Installations#flatpak-installation)
>
> For NixOS, see instructions [here](/Alternative-Installations#nixos-installation)  
> For the Steam Deck, see instructions [here](/Alternative-Installations#steam-deck-installation)

## Installation Steps

1. Download our [LUG Helper](https://github.com/starcitizen-lug/lug-helper/releases/latest) (Distro packages are listed [here](https://github.com/starcitizen-lug/lug-helper#installation))
2. [Launch](Tips-and-Tricks#how-to-run-the-lug-helper) the LUG Helper and select `Install Star Citizen`
3. Allow the Preflight Check to fix any issues it finds before proceeding!
4. Install the Wine prefix (this directory contains the game) to any linux-formatted partition.
5. After the install completes, run the RSI Launcher, log in, and click Install to finish installing the game. **Do not** change the default install location `C:\Program Files\Roberts Space Industries`!
6. Launch the game. See you in the 'verse!

## After Installation

{: .warning-title }
> Important Configuration
> - Set your [keyboard layout](Troubleshooting/mouse-keyboard-issues#non-us-keyboard-keys-not-working) for non-US compatability with common keybinds
> - Nvidia users: See [troubleshooting guide](Troubleshooting/nvidia#severe-frame-drops) to resolve severe frame drop issues
> - Wayland users: See [required workarounds](Troubleshooting/mouse-keyboard-issues#mousecursor-warp-issues-and-view-snapping-in-interaction-mode) to resolve window and cursor issues
> - Bookmark the wiki [latest news](/#news) to keep up with current recommendations

{: .tip-title }
> Customization
> - Enable NVIDIA [DLSS](Troubleshooting/nvidia#dlss-deep-learning-super-sampling)
> - Set up your [Sticks, Throttles, & Pedals](Sticks,-Throttles,-&-Pedals)
> - Set up your [Head Tracking](Head-Tracking)

{: .note-title }
> Questions or Problems?
>
> - Check our [Troubleshooting Guide](Troubleshooting) or ask for help in one of our [social channels](/#join-us)!
