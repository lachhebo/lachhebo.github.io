---
title: "Setup an Evoluent Vertical Mouse for MacOs"
date: 2020-12-16
---

The Evoluent Vertical mouse is probably one of the best vertical mouses on the market and I could easily advise you to use it if your interested in this kind of products. However, the Evoluent team was not able to develop macOS driver for the mouse. So by default, we can't remap the mutliple buttons of the mouse. Thanskfully the open source community developed a program for macOS called [Karabiner](https://karabiner-elements.pqrs.org/) which can do wonders here. You can easily install it and then use the configuration file below to use the evoluent mouse with my configuration.

My config file for karabiner can be downloaded through this link <a href="https://raw.githubusercontent.com/lachhebo/lachhebo.github.io/screenshots/download/karabiner.json" download>karabiner.json</a>. Put it here *~/config/karabiner/karabiner.json*.

 Below, I go more in depth about how I configured the mouse.

<img height="350" src="https://raw.githubusercontent.com/lachhebo/lachhebo.github.io/screenshots/evoluent_mouse.jpg" />

## Switch between workspace

The first rule to add to make the mouse tolerable in macOS is the rule allowing switching between workspaces, just like you can do using a macbook trackpad. Hence, we are mapping a press to the edge button to switch to left or right workspace.

```json
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
```

## Invoke Mission Control

Here, we map a long press to the middle button mouse to launch the mission control view.

```json
    {
        "from": {
            "pointing_button": "button3"
        },
        "to_if_held_down": {
            "key_code": "mission_control"
        },
        "type": "basic"
    },

```

Additionnaly, I decreased the time to press on button middle before launching the mission control view.

```json
    "basic.to_if_held_down_threshold_milliseconds": 300,
```

## Go back or Go forward

Eventually, we map a press to middle button simultaneously used with a press to an edged button to go back or go forward. Mostly, it is useful when using a browser to go back to the previous visited page.

```json
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
```

## Conclusion

the complete file is

```json
{
    "global": {
        "check_for_updates_on_startup": true,
        "show_in_menu_bar": true,
        "show_profile_name_in_menu_bar": false
    },
    "profiles": [
        {
            "complex_modifications": {
                "parameters": {
                    "basic.simultaneous_threshold_milliseconds": 50,
                    "basic.to_delayed_action_delay_milliseconds": 500,
                    "basic.to_if_alone_timeout_milliseconds": 1000,
                    "basic.to_if_held_down_threshold_milliseconds": 300,
                    "mouse_motion_to_scroll.speed": 100
                },
                "rules": [
                    {
                        "description": "Set lower button to back and upper to forward",
                        "manipulators": [
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
                            {
                                "from": {
                                    "pointing_button": "button3"
                                },
                                "to_if_held_down": {
                                    "key_code": "mission_control"
                                },
                                "type": "basic"
                            },
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
                        ]
                    }
                ]
            },
            "devices": [
                {
                    "disable_built_in_keyboard_if_exists": false,
                    "fn_function_keys": [],
                    "identifiers": {
                        "is_keyboard": false,
                        "is_pointing_device": true,
                        "product_id": 401,
                        "vendor_id": 6780
                    },
                    "ignore": false,
                    "manipulate_caps_lock_led": false,
                    "simple_modifications": []
                },
                {
                    "disable_built_in_keyboard_if_exists": false,
                    "fn_function_keys": [],
                    "identifiers": {
                        "is_keyboard": true,
                        "is_pointing_device": false,
                        "product_id": 615,
                        "vendor_id": 76
                    },
                    "ignore": true,
                    "manipulate_caps_lock_led": true,
                    "simple_modifications": []
                },
                {
                    "disable_built_in_keyboard_if_exists": false,
                    "fn_function_keys": [],
                    "identifiers": {
                        "is_keyboard": true,
                        "is_pointing_device": false,
                        "product_id": 34304,
                        "vendor_id": 1452
                    },
                    "ignore": true,
                    "manipulate_caps_lock_led": true,
                    "simple_modifications": []
                },
                {
                    "disable_built_in_keyboard_if_exists": false,
                    "fn_function_keys": [],
                    "identifiers": {
                        "is_keyboard": true,
                        "is_pointing_device": false,
                        "product_id": 636,
                        "vendor_id": 1452
                    },
                    "ignore": true,
                    "manipulate_caps_lock_led": true,
                    "simple_modifications": []
                }
            ],
            "fn_function_keys": [
                {
                    "from": {
                        "key_code": "f1"
                    },
                    "to": {
                        "consumer_key_code": "display_brightness_decrement"
                    }
                },
                {
                    "from": {
                        "key_code": "f2"
                    },
                    "to": {
                        "consumer_key_code": "display_brightness_increment"
                    }
                },
                {
                    "from": {
                        "key_code": "f3"
                    },
                    "to": {
                        "key_code": "mission_control"
                    }
                },
                {
                    "from": {
                        "key_code": "f4"
                    },
                    "to": {
                        "key_code": "launchpad"
                    }
                },
                {
                    "from": {
                        "key_code": "f5"
                    },
                    "to": {
                        "key_code": "illumination_decrement"
                    }
                },
                {
                    "from": {
                        "key_code": "f6"
                    },
                    "to": {
                        "key_code": "illumination_increment"
                    }
                },
                {
                    "from": {
                        "key_code": "f7"
                    },
                    "to": {
                        "consumer_key_code": "rewind"
                    }
                },
                {
                    "from": {
                        "key_code": "f8"
                    },
                    "to": {
                        "consumer_key_code": "play_or_pause"
                    }
                },
                {
                    "from": {
                        "key_code": "f9"
                    },
                    "to": {
                        "consumer_key_code": "fast_forward"
                    }
                },
                {
                    "from": {
                        "key_code": "f10"
                    },
                    "to": {
                        "consumer_key_code": "mute"
                    }
                },
                {
                    "from": {
                        "key_code": "f11"
                    },
                    "to": {
                        "consumer_key_code": "volume_decrement"
                    }
                },
                {
                    "from": {
                        "key_code": "f12"
                    },
                    "to": {
                        "consumer_key_code": "volume_increment"
                    }
                }
            ],
            "name": "Default profile",
            "parameters": {
                "delay_milliseconds_before_open_device": 1000
            },
            "selected": true,
            "simple_modifications": [],
            "virtual_hid_keyboard": {
                "country_code": 0,
                "mouse_key_xy_scale": 100
            }
        }
    ]
}
```
