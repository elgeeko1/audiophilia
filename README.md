# Stereo Blaster as a Service

Web service that can be configured to control devices, such as stereo amplifiers, through infrared remote control. Use for remote control of stereos from a desktop browser, mobile browser, or map to keyboard keys or mouse buttons. Scroll up to jam out, y'all!

## Why this Exists

My audio setup includes a USB output device that doesn't have digital volume control, which means I can only use the volume knob on my amplifier. And that's... way, over there. Unacceptable.

## What this Is

Ansible scripts to configure a Linux target with:

- Drivers for an IR transmitter ('blaster') via lirc
- Node server and module lirc_web to translate web requests to IR commands

## What this Isn't

Maintained, expected to work, or documented.
