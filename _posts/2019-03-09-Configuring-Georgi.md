---
layout: post
title: Configuring Georgi
desc: How to modify your keymap, chords, and other Georgi specfics.
tags: [Georgi]
---

# Georgi Configuration

Awesome, now that you've figured out the convoluted shitshow that is Georgi, let's get on making it usable for you! A little forward is necessary here, if you've used QMK before, Georgi does some very unQMK things.

# The Future
We're currently working with the QMK team to develop a front end that is compatible with the [QMK configurator](http://config.qmk.fm). Once this is done, configuring Georgi or other steno boards from the browser will be possible. Until then, we need to set up the build environment. [So give this a diddle and come on back.](https://github.com/qmk/qmk_firmware/blob/master/docs/getting_started_build_tools.md).

# Structure of a keymap
Good on you for getting that all set up!

Take a second to familarize yourself with this [example keymap](https://github.com/germ/qmk_firmware/blob/georgi/keyboards/georgi/keymaps/default/keymap.c). Look a little funky? I told you it would be a little weird.

Let's start with the entry point will be called during processing, **processQwerty()** is called anytime a Symbol or Qwerty button is to be looked up. The easiest way to think of this is as a small dictionary onboard your keyboard. In steno mode we just send the steno chords, in Qwerty mode we perform a lookup against this list. That's literally it (for now anyway).

There are two parts to every entry a trigger and an action.

# Triggers
A trigger looks like this 'LSD | LK | LW | LR', the pipe character is used to glue the various keys together. The first letter is the side of the board, the second the steno key it corresponds to, the exception is LSUp, LSDown, and LFT (as LT is already defined). A list is provided below.

![georgi keymap](/img/georgi/defines.png)

We will talk about triggers in a little bit again later on.

# Actions
One a trigger is matched, an action is taken. Any valid C code can be in there, but usually you'll want to use the **SEND()** function to press keys from the [QMK Keycode List](https://github.com/qmk/qmk_firmware/blob/master/docs/keycodes.md) or use SEND_STRING() to [output some text](https://github.com/qmk/qmk_firmware/blob/master/docs/feature_macros.md). SEND_STRING can also be used to send modifiers such as control, push buttons, delay and all sorts of fun stuff. A good idea is to try a small modification to a existing action before going insane :)

# Callers
There are two different callers that can respond to a chord: P (Press) and PJ (Press Non Jumping). The dictionary is looked up from the top top the bottom, on the first match it finds it runs the action and may halt further processing. 

P will execute an action and halt further processing. P only works on an exact match, so any partial chords are ignored.

PJ will remove it's trigger from a chord once it's found, and add it's presses to the the output. Typically PJ is used for modifiers such as shift, control, etc. Due to the nature of it, anything that relies on matching a chord that will be removed by a matching partial chord must be placed before any conflicting PJs. Due to this the typical structure is:

- Conflicting Chords
- Modifiers/PJs
- Whole bunch of Ps

# Layers
Unlike normal QMK boards, we can get away with only using a single layer and prefixing defined chords as "layers". This is done by a few defines at the top like so `#define FUNCTION (LSU | LSD | ST3)`. This will create a pseudo layer prefix chord that we can use elsewhere, for example: `P(FUNCTION | ST4, SEND_STRING("TEST"));` would send "TEST" when LSU, LSD, ST3, and ST4 are pressed. This is used in the default keymap for layers like Media and Movement.

# Special Handling
The toggles that control switching modes and all that are hardcoded. To modify these you need to jigger sten.h. 

# Building
Once your changes are complete, you can build your hex file by simply running `make georgi` from the root directory of your QMK firmware folder, this will compile and build hex files for all keymaps in the georgi folder. You can specify a keymap to build like so: `make georgi:default`, where default is the name of the map to build.

Have fun!
