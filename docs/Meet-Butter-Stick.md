---
nav_order: 9
layout: post
title: Meeting Butterstick
desc: Butterstick Quickstart Guide
tags: [Butterstick]
---

# Unboxing Butterstick
Thanks for buying one of these little guys, it's a little wonky but I'm sure you'll have some fun with it!

In your package you should have recieved a populated PCB ready for your switches and caps. Go ahead and get those installed if you have not!
A note, try and use lighter switches then you would normally. Gateron Clears are a good start or any MX spring swapped down to 20cN should be perfect.

# Modes
There is a ton of overlap with the Georgi firmware, after you get your board set up and start mucking about with your FW go read [Hacking Georgi](/Hacking-Georgi/).

This is the default layout, for keys inbetween press both keys to trigger it. For the blue circles, all four in that area.
### Update: Backspace is VBNM! Forgot to include it in the maps
![default layout](/img/butterstick/layout.png)

There are a few other 'layers' as well, the coloured keys are the prefix for the chord!
![Layers](/img/butterstick/layers.png)

# Command Mode

Due to the size of the board, key combos can be a pain if there is a conflict. What do you do when the key you're trying to chord overlaps with another that you need? Enter Command mode. Command mode buffers all of the keys that are pressed while it's active; once you exit command mode the keys are all pressed down, and then released in one go. So inserting say 'Ctrl+Shift+S' could be done in the following way 'Command Mode/Ctrl/Shift/S/Command Mode'.

Note: There are a good number of alternative binds for modifiers and you can always add definitions to your firmware! If you find a bind that you're using frequently, don't just whack it in over and over again in command mode, add it to your keyboard!

# Entering QMK (Gaming mode)

Pressing this chord will move to the next avalible QMK layer (or do nothing if you only have the base layer). This layer acts like a traditional keyboard as opposed to stenotype. On this layer are your traditional WASD. You may want to modify this to suit your gaming needs. To exit back to normal mode press the right bottom corner button.

# Protips
- Do yourself a favour and print off the [keyboard map](/img/butterstick/layout.png) and leave it by your desk. This little guy is a radical departure from usual keyboards and with any new map, it's going to take some getting used to. Looking stuff up is to be expected for the first bit and getting used to the keyboard itself is going to take a while even for existing stenographers!
