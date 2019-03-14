---
layout: post
title: Hacking Georgi
desc: All the dirty stuff you need to know about the system to really break it.
tags: [Georgi]
---

# Hacking Georgi
Alright, so you've finally found something that you can't do from the default firmware. A bit of heads up here you're going to need to know some QMK internals so [give this excellent guide a read](https://beta.docs.qmk.fm/for-a-deeper-understanding/understanding_qmk) and come on back.

# How Georgi Do
Pop open sten.h so you have a reference to use. Everything that Georgi does is independant of QMK proper and happens in here and processQwerty() in the keymap. The current chord state is held in a cChord. We hook `process_steno_user` to update this chord as keys come in and hook `send_steno_chord_user` to process everything once the keys are up. If none of our actions match we return true and continue processing (QMK will then send the steno codes).

## cChord
This is just a bigass bitfield that is set in `process_steno_user` we can add keys to this easily but there are a total maximum of 32 possible states we can jam in there. To define your own codes append a entry to the ORDER enum, make a nice pretty #define for it and start adding entries to your keymap.

## Key Repeat
Once the first button press comes in we start a timer and keep checking it in `matrix_scan_user`, if this timer expires we send the lookup the current chords and reset the timer. 

## Mouse Keys
Mousekeys are done using the repeat mechanism, if a mousepress is sent it will remain in a down state until the chord is sent. The button that is clicked is selected from [this list here](https://github.com/qmk/qmk_firmware/blob/master/docs/keycodes.md#mouse-keys)

## Send
Send is just a light wrapper around register_code(), this is needed to buffer if we are in command mode. Just like register_code()

## Command mode
The buffer can store up to 20 different keypresses (if you somehow need more, update config.h). The way we do this is by 

In addition to the handling logic, the following functions are currently provided.

**clickMouse**: Send


