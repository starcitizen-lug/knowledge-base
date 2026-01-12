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
> See our [Recommended Distros](Tips-and-Tricks#recommended-distros) for a list of distros most compatible with Star Citizen.

{: .note-title }
> Immutable Distros
> 
> For immutable distros other than Bazzite, we recommend the [flatpak installation](Alternative-Installations#flatpak-installation). For NixOS, see [here](/Alternative-Installations#nixos-installation). For the Steam Deck, see [here](/Alternative-Installations#steam-deck-installation).

## Installation Steps

1. Download our [LUG Helper](https://github.com/starcitizen-lug/lug-helper/releases/latest) (Distro packages are listed [here](https://github.com/starcitizen-lug/lug-helper#installation))
2. [Launch](Tips-and-Tricks#how-to-run-the-lug-helper) the LUG Helper and select `Install Star Citizen`.
3. Allow the Preflight Check to fix any issues it finds before proceeding!
4. When the Helper asks, select a location for the Wine prefix on a Linux partition with approximately 150GB available. This directory will contain the game. Avoid HDDs and NTFS filesystems.
5. After the install completes, run the RSI Launcher, log in, and click Install to finish installing the game. **Do not** change the default install location `C:\Program Files\Roberts Space Industries`!
6. Launch the game. See you in the 'verse!

## After Installation

{: .warning-title }
> Important Configuration
> - Configure zram to match [our recommendations](/Performance-Tuning#zram--swap) if you have less than 64GB ram.
> - For non-US keyboard layouts, [enable compatibility](Troubleshooting/mouse-keyboard-issues#non-us-keyboard-keys-not-working) with common game keybinds.
> - Nvidia users: See our [troubleshooting guide](Troubleshooting/nvidia#severe-frame-drops) to resolve severe frame drop issues.
> - Wayland users: See [required workarounds](Troubleshooting/mouse-keyboard-issues#mousecursor-warp-issues-and-view-snapping-in-interaction-mode) to resolve window and cursor issues.
> - Bookmark our wiki's [latest news](/#news) to keep up with current recommendations.

{: .tip-title }
> Performance and Customization Options
> - Enable NVIDIA [DLSS](Troubleshooting/nvidia#dlss-deep-learning-super-sampling).
> - Set up your [Sticks, Throttles, & Pedals](Sticks,-Throttles,-&-Pedals).
> - Set up your [Head Tracking](Head-Tracking).
> - See [Performance Tuning](/Performance-Tuning) and [Tips and Tricks](/Tips-and-Tricks) for additional post-install recommendations.

{: .note-title }
> Questions or Problems?
>
> - Check our [Troubleshooting Guide](Troubleshooting) or ask for help in one of our [social channels](/#join-us)!
