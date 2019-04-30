---
layout: post
title: Hacking Georgi
desc: All the dirty stuff you need to know about the system to really break it.
tags: [Georgi]
---

# Hacking Georgi
Alright, so you've finally found something that you can't do from the default firmware. A bit of heads up here, you're going to need to know some QMK internals so [give this excellent guide a read](https://beta.docs.qmk.fm/for-a-deeper-understanding/understanding_qmk) and come on back.

### How Georgi Do
Pop open sten.h so you have a reference to use. Everything that Georgi does is independent of QMK proper and happens in here and processQwerty() in the keymap. The current chord state is held in a cChord. We hook `process_steno_user` to update this chord as keys come in and hook `send_steno_chord_user` to process everything once the keys are up. If none of our actions match we return true and continue processing (QMK will then send the steno codes).

### cChord
This is just a bigass bitfield that is set in `process_steno_user` we can add keys to this easily but there are a total maximum of 32 possible states we can jam in there. To define your own codes, append an entry to the ORDER enum, make a nice pretty #define for it, and start adding entries to your keymap.

### Key Repeat
Once the first button press comes in we start a timer and keep checking it in `matrix_scan_user`, if this timer expires we send the lookup the current chords and reset the timer. You can adjust this timer by changing the REP_DELAY #define in sten.h.

### CLICK_MOUSE()
Mousekeys are done using the repeat mechanism, if a mousepress is sent it will remain in a down state until the chord is sent. The button that is clicked is selected from [this list here](https://github.com/qmk/qmk_firmware/blob/master/docs/keycodes.md#mouse-keys). If the chord is too short to register a repeat a single click is generated.

### SEND()
Send is just a light wrapper around register_code(), this is needed to buffer if we are in command mode. Just like register_code() Quantum Codes cannot be used here. You need to use SEND otherwise command mode won't work!

### SET_STICKY()
When this chord is matched a sticky bit is set in cChord. The usual way you would use this is with the codes RES1 and RES2. When the sticky bit is set cChord will process all incoming chords with this. Use cases are similar to changing the default layer in QMK. Using sticky bits you could toggle between QWERTY and WORKMAN and whatnot. To clear any stickybits that have been set, pass 0 when calling it.

### SWITCH_LAYER()
This is a helper that jumps to the specified QMK layer, if it exists. Returning to the default layer is left as a excercise to the reader.

### Command mode
The buffer can store up to 20 different keypresses (if you somehow need more, update **REP_DELAY**). The way we do this is by wrapping **register_code()** with send and replaying the buffer, depressing every key in the sequence before key up. This only applies to wrapped codes so things like mouse clicks and custom code won't be in there.

### QWERTY Fallback
proessFakeSteno() simply maps chords to NKRO Plover as a fallback mode. Ideally we would have a datastructure for various dictionaries but switching the called lookup table seems to be fine. This is a young project, submit a PR.

### Adding functionality
All of the logic happens in **process_steno_chord_user**, this should be your main place to add/augment functionality. In here you can preprocess chords before passing them off for handling, enable toggles, disable features, etc. You need to remember that just like in any dictionary, there is a order that everything is evaluated in, so be careful.

Two exit points are provided to jump to, **out** which halts further processing and cleans up, and **steno** which will clean up and pass off the chords to Plover. Local gotos are okay, get at me.

### Other QMK jazz
There's a ton of stuff that can be leveraged here. Take a look through the tmk/common folder for some ideas and weird whacky keyboards you see around. This is a computer, make it do weird shit! If you need a hand reach out, I'll warn you I suck at steno though.
