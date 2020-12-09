---
layout: post
title: "Setup an Evoluent Vertical Mouse for MacOs"
date: 2020-04-16
categories: MacOS Hardware
published: true
---


The Evoluent Vertical mouse is probably one of the best vertical mouse on the market and I could easily advise you to use it if your interesseted by this kind of product. However, the Evoluent team was not able to develop macos driver for the mouse. So by default, we can't remap the mutlitple buttons of the mouse. Thanskfully the open source community develop a program for macOS called [Karabiner](https://karabiner-elements.pqrs.org/) who can do wonders in our case. You can easily install it and then use this configuration file to use the evoluent mouse with my configuration.

![Evoluent mouse](/assets/evoluent_mouse.jpg)

My config file for karabiner can be download through this link [karabiner.json](/assets/download/karabiner.json). Put it here *~/config/karabiner/karabiner.json*.

 Below, I go more in depth about how I configured the mouse.

## Switch between workspace

The first rule to add to make the mouse tolerable in macos is the one that allows switching between workspaces like you can do it using a macbook trackpad. Hence, we are a mapping a press to the edge button to switch to the left or right workspace.

    {
        "from": {
            "pointing_button": "button4"
        },
        "to": {
            "key_code": "right_arrow",
            "modifiers": [
                "control"
            ]
        },
        "type": "basic"
    },
    {
        "from": {
            "pointing_button": "button6"
        },
        "to": {
            "key_code": "left_arrow",
            "modifiers": [
                "control"
            ]
        },
        "type": "basic"
    }

## Invoke Mission Control

Here, we map a long press to the middle button mouse to launch the mission control view.

    {
        "from": {
            "pointing_button": "button3"
        },
        "to_if_held_down": {
            "key_code": "mission_control"
        },
        "type": "basic"
    },

Additionnaly, I decreased the time to press on button middle before launching the mission control view.

    "basic.to_if_held_down_threshold_milliseconds": 300,

## Go back or Go forward

Eventually, we map a press to middle button simultaneously used with a press to an edged button to go back or go forward. Mostly, it is useful when using a browser to go back to the previous visited page.

    {
        "from": {
            "simultaneous": [
                {
                    "pointing_button": "button3"
                },
                {
                    "pointing_button": "button4"
                }
            ]
        },
        "to": {
            "key_code": "right_arrow",
            "modifiers": [
                "command"
            ]
        },
        "type": "basic"
    },
    {
        "from": {
            "simultaneous": [
                {
                    "pointing_button": "button3"
                },
                {
                    "pointing_button": "button6"
                }
            ]
        },
        "to": {
            "key_code": "left_arrow",
            "modifiers": [
                "command"
            ]
        },
        "type": "basic"
    },
