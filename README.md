# Stereo Blaster as a Service

An example web service that can be configured to control devices, such as stereo amplifiers, through infrared remote control. Use for remote control of stereos from a desktop browser, mobile browser, or map to keyboard keys or mouse buttons. Scroll up to jam out, y'all!

You will need to customize this for your setup -- this won't work out of the gate. Time to put your thinking cap on.

The code in this repository provisions a Linux computer with a web server that transmits IR signals over a USB transmitter ('blaster). I've tested this on x86_64 but presumably this should work on ARM targets such as a Raspberry Pi.


## Why this Exists

My audio setup includes a USB output device that doesn't have digital volume control, which means I can only use the volume knob on my amplifier. And that's... way, over there. Unacceptable.


## What this Is

Ansible scripts to configure a Linux target with:

- Drivers for an IR transmitter ('blaster') via lirc
- Dockerized node server and module lirc_web to translate web requests to IR commands
- Two remote code configurations:
- - Yahama RAS-13 remote (AS-301 and AS-501 amplifiers)
- - SMSL RC-1 remote (SMSL m500 and others)

Optionally I included a Roon Server role but this is not required for the IR blaster.

## What this Isn't

Maintained, expected to work, or documented.


# Hardware

- USB IR blaster: https://www.irblaster.info/usb_blaster.html


# Resources

- https://www.npmjs.com/package/lirc_web
- https://github.com/alexbain/lirc_web
- https://www.mythtv.org/wiki/FTDI_USB_IR_Blaster_/_Transmitter_using_LIRC
- http://alexba.in/blog/2013/02/23/controlling-lirc-from-the-web/
