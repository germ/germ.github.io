---
layout: post
title: Configuring Georgi
desc: How to modify your keymap, chords and other Georgi specfics.
tags: [Georgi]
---

# Georgi Configuration

Awesome, now that you've figured out the convoluded shitshow that is Georgi, let's get on making it usable for you! A little foreword is necessary here, if you've used QMK before, Georgi does some very unQMK things.

# Structure of a keymap
Take a second to familarize yourself with this [example keymap](https://github.com/germ/qmk_firmware/blob/softlove/keyboards/georgi/keymaps/default/keymap.c). Look a little funky? I told you it would be a little weird.

Let's start with the entry point will be called during processing, processQwerty() is called anytime a Symbol or Qwerty button is to be looked up. The easiest way to think of this is as a small dictionary onboard your keyboard. In steno mode we just send the steno chords, in Qwerty mode we perform a lookup against this list. That's literally it (for now anyway).

There are two parts to every entry a trigger and an action.

# Triggers
A trigger looks like this 'LSD | LK | LW | LR', the pipe character is used to glue the various keys together. The first letter is the side of the board, the second the steno key it corresponds to, the exception is LSUp, LSDown, and LFT (as LT is already defined). A list is provided below.

![georgi keymap](/img/georgi/defines.png)

We will talk about triggers in a little bit again.

# Actions
One a trigger is matched a action is taken. Any valid C code can be in there, but usually you'll want to use the register_code() function to press keys from the [QMK Keycode List](https://github.com/qmk/qmk_firmware/blob/master/docs/keycodes.md) or use SEND_STRING() to [output some text](https://github.com/qmk/qmk_firmware/blob/master/docs/feature_macros.md). SEND_STRING can also be used to send modifiers such as control, push buttons, delay and all sorts of fun stuff. A good idea is to try a small modification to a existing action before going insane :)

# Callers
There are two different callers that can respond to a chord P (Press) and PJ (Press Non Jumping). The dictionary is looked up from the top top the bottom, on the first match it f
