---
nav_order: 4
description: Development Firmwares for Georgi
layout: post
title: Georgi Firmwares
---

# Current QMK Master Build

[Download Current](https://qmk.fm/compiled/georgi_default.hex){: .btn .btn-primary}

# How to flash
Install QMK Toolbox, download the desired firmware, actuate the button on the left PCB (with the mini-USB port) to enter 'Bootloader Mode', and then follow [this guide](https://www.youtube.com/watch?v=VR53Wo9Z960)

**You can check what your current firmware is by pressing #-TSDZ (all on the right-side PCB that has no mini-USB port) in QWERTY mode.**

**Note: If you aren't testing Beta Builds, don't flash the firmwares below!**
## Version 1.1 ClayM:[Download](/fw/georgi_v1_1.hex)
	- Mid-QWERTY stroke improvements
	- Added Partial Chords 
	- Added Sticky Bits

## Version 1.1 ClayM-Flipped:[Download](/fw/georgi_v1.1-Flipped.hex)
	- Same as 1.1, but with flipped number keys as the stenographers seem to enjoy

## Version 1, Stenoknight: [Download](/fw/georgi_RC01_Wilfred.hex)
	- Literally the same as the RC!

## Alpha 03, TomatoSoup: [Download](/fw/georgi_0.03_TomatoSoup.hex)
	- Major QWERTY mode improvements, now handles continuous typing
	- Optimized code size for extra space
	- Reworked chord processing backend
	- Removed duplicate chords

## Alpha 02, Frag: [Download](/fw/georgi_0.02_Frag.hex)
	- Fixed Gaming mode toggle
	- Separated NUM keys

## Alpha 01, Ted: [Download](/fw/georgi_0.01_Ted.hex)
	- Initial Release

# How to get devel; contribute or hack on your chords
I maintain a branch on GitHub for all my development work, this is where we submit PRs to QMK master from. 

To get devel:
```
git clone https://github.com/germ/qmk_firmware.git
make gboards/k/georgi:default:dfu
```

If you make changes, come up with funky layouts and all that. Submit a PR and we'll merge it and bundle it together with our next push to master!
