---
layout: post
title: USB Enumeration
tags: linux usb protocol
categories: usb
---
It is about usb enumaration...

### What is usb enumeration?
Host PC want to know the usb device.
Who is it? What is it? What can it do?

For every usb device, it has many descriptors, which describe itself...
to answer above qusetions...

USB enumeration is the process to know the device (through control endpoint/pipe).
And choose/set the device's configuration/interface/functions.
Change the device's machine-state to ready state!!

After usb enumeration, usb host can use device-node to communication with the usb device
through common/specified protocols...

### What's the descriptors?
USB device has many descriptors to describe it self...
Usually, below descriptors are standard and common.
device descriptor! configuration decriptor! interface descriptor! endpoint descriptor!
string descriptor!

Obviously, the descriptors is stored in the rom code (usb dongle?)
Or generated dynamically by the code, such as linux usb gadget device.
Yes, descritors are programmed in some platform.

### What's else?
The most important for usb device is:
1. descriptor
2. function code

Yes, descriptor let host know what you are, and which driver need to be loaded.
But the function logic/code is more important!!
It should refer to the specified protocols.

For example, if you want to implement a UVC function driver!!
You should implement the UVC control/streaming request!!
Such as bright/AAA/White Balance/resoution/framerate settings, through control block.
Data IN request for streaming requirement!!

### To be continued...
