---
layout: post
title: Georgi Firmwares
desc: Development Firmwares for Georgi
tags: [Georgi]
---

**Note: If you aren't testing Beta Builds, you don't want to flash these **
**You can check what your current firmware is by pressing #-TSDZ in QWERTY mode**


# Alpha 02, Frag: [Download](/fw/georgi_0.02_Frag.hex)
	- Fixed Gaming mode toggle
	- Seperated Num keys

# Alpha 01, Ted: [Download](/fw/georgi_0.01_Ted.hex)
	- Initial Release

# How to flash
Install QMK Toolbox, download your firmware and follow [this guide](https://www.youtube.com/watch?v=VR53Wo9Z960)

# How to get devel, contribute or hack on your chords
I maintain a branch on github for all my development work, this is where we submit PRs to QMK master from. To get it.

~~~~
git clone https://github.com/germ/qmk\_firmware.git
git checkout georgi
make georgi:default:dfu
~~~~

If you make changes, come up with funky layouts and all that. Submit a PR and we'll merge it and bundle it together with our next push to master!
