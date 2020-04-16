---
layout: post
title: "Use an Apple Magic Trackpad on Linux"
date:   2020-03-30
categories: Linux Hardware
published: true
---




### How to use a Apple Magic Trackpad on Linux ? 


Currently, the Apple magic trackpad is probably one or the best bluetooth trackpad on the market. Unfortunately, using it on Linux can still be a bit of a pain.

If it is not a problem anymore to pair the device with the computer, the trackpad will probably not correctly repond to the order you will give to it at first. 

Most user would sadly conclude that the device is not working on Linux and would pick an another trackpad but not me (and may be not you). I went on the Internet on looked after a solution until i found this great Github repository :

- https://github.com/robotrovsky/Linux-Magic-Trackpad-2-Driver

The solution they gave for 'pressure' issue was to create a 90-magic-trackpad.conf in the /usr/share/X11/xorg.conf.d folder who look like that :

    Section "InputClass"
            Identifier      "Touchpads"
            Driver          "libinput"
            MatchProduct    "Apple Inc. Magic Trackpad 2"
            MatchDevicePath "/dev/input/event*"
    EndSection


It did not work, so i looked at the file already present in this folder and found the 10-quirks.conf who looked like that :  


    # Collection of quirks and blacklist/whitelists for specific devices.
    
    # Accelerometer device, posts data through ABS_X/ABS_Y, making X unusable
    # http://bugs.freedesktop.org/show_bug.cgi?id=22442 
    Section "InputClass"
            Identifier "ThinkPad HDAPS accelerometer blacklist"
            MatchProduct "ThinkPad HDAPS accelerometer data"
            Option "Ignore" "on"
    EndSection
    
    # https://bugzilla.redhat.com/show_bug.cgi?id=523914
    # Mouse does not move in PV Xen guest
    # Explicitly tell evdev to not ignore the absolute axes.
    Section "InputClass"
            Identifier "Xen Virtual Pointer axis blacklist"
            MatchProduct "Xen Virtual Pointer"
            Option "IgnoreAbsoluteAxes" "off"
            Option "IgnoreRelativeAxes" "off"
    EndSection
    
    # https://bugs.freedesktop.org/show_bug.cgi?id=55867
    # Bug 55867 - Doesn't know how to tag XI_TRACKBALL
    Section "InputClass"
            Identifier "Tag trackballs as XI_TRACKBALL"
            MatchProduct "trackball"
            MatchDriver "evdev"
            Option "TypeName" "TRACKBALL"
    EndSection
    
    # https://bugs.freedesktop.org/show_bug.cgi?id=62831
    # Bug 62831 - Mionix Naos 5000 mouse detected incorrectly
    Section "InputClass"
            Identifier "Tag Mionix Naos 5000 mouse XI_MOUSE"
            MatchProduct "La-VIEW Technology Naos 5000 Mouse"
            MatchDriver "evdev"
            Option "TypeName" "MOUSE"
    EndSection

I conclude i just needed to add the Apple MagicTrackpad configuration in this file and it worked perfectly :). Actually, to enable the to enable touch to click, i also add the line :

    Option          "Tapping" "on"


As a final step, to avoid that anyone would once again loose one or two hours trying to use a simpel trackpad; i filled a bug report at fedora bugzilla available at this [address](https://bugzilla.redhat.com/show_bug.cgi?id=1818982) 


### Conclusion 

I think it was a good example of how sometimes a Linux user can cope with an issue and report the problem to help others people not facing it.  
