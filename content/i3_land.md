---
layout: post
title: "testing a tiling window manager for a week on thinkpad"
date:   2020-05-17
published: true
---

In the last few years, tiling window manager gathered a lot of traction, they are presumed to be extremely lightweight, run responsively even with old hardware and more importantly improve your productivity. I have been using gnome-shell and plasma on my thinkpad T460 for the last few years. I sometime felt frustated by the unresponsiveess of my computer and i am always looking for new way of improving my productivity so the tiling window manager world caught my attention.

Using a tiling window manager means 100% of your screen is always used, the workflow depend heavily on keyboard shortcuts, The windows size and position are dynamically changed every time a new window is opened on the workspace.

The first step is to choose a tiling window manager, there are tons of them :

- i3wm
- dwm
- awesome
- xmonad
- ...

The most famous of them being i3, this is the one I decided to use.

### Installation

The installation process was pretty fast :

     sudo dnf install i3 i3status dmenu i3lock xbacklight feh 

Firstly, i3 play well when installed next to gnome-shell, it is available in the list of desktop environnement (on the logging page) and gnome-shell continue to work without any issue or sluggishness when i3 is installed on the system. This is not the case when plasma is installed next to it as it is adviced to not install both desktop environnement on the system at the same time.

When starting i3 session, i easily followed steps of the welcome screen and start reading the configuration file as I was testing it. Default configuration are pretty good but depending on your hardware, many things won't work by default. On mine which is a thinkpad, I had to do a lot of things, let's review some issue i encontered.

### Fix

The most annoying issue was with the screen management, I heard that tiling window manager play nicely with multiple monitor setup. Definetely not in my case, the issue with i3 is it will not dynamically adjusting when my monitor setup change, I need to run one or two xrandr command line to handle every modification of my screen setup. When I connect  a monitor and when I disconnect it. Same thing if I decide to close the lid of my laptop to only use the external monitor or when I open it. Those kinds of modifications can happened dozens of times in a single day and it's a real burden to handle this manually. Samething with wallpaper because i also need to run a feh command in that case.

    xrandr --output HDMI-2 --right-of eDP-1 --mode 2560x1440

Furthermore, dmenu was not working and did not display flatpak apps, so you need to use i3-dmenu-desktop instead

    sudo dnf install i3-dmenu-desktop

Eventually, I installed brighnessctl as xbacklight was not working and used it to control my brightness.

 bindsym XF86MonBrightnessUp exec --no-startup-id brightnessctl set +10%
    bindsym XF86MonBrightnessDown exec --no-startup-id brightnessctl set 10%-

- If there is an applet to handle the wifi which play well with i3, there is no functional bluetooth applet (at least one I heard of) and bluetooth became a major thechnology in the few last years. The only solution I find on the web is blueman which does not fit well with tiling window manager.

### Configuration

When moving a window to a workplace, I want to move to that workspace; hence I changed the config file

    bindsym $mod+Shift+1 move container to workspace number $ws1; workspace number $ws1
    bindsym $mod+Shift+eacute move container to workspace number $ws2; workspace number $ws2

I changed the bar config to use another font, however I was not sucessful at displaying the bar with transparency effect

    bar {
            font pango:FontAwesome-10 10
            status_command i3status --config ~/.config/i3/i3status.conf
            position bottom
            i3bar_command i3bar --transparency
            tray_output primary
            workspace_min_width 20
    }

Setup my wallpaper

    exec --no-startup-id  feh --bg-scale ~/Images/elephant_trunk_bird.jpg

 Start redhsift at startup (a night mode filter software) :

    exec --no-startup-id "redshift"

Be sure you have every needed fonts, any missing may cause issues :

    sudo dnf install levien-inconsolata-fonts
    sudo dnf install mozilla-fira-mono-fonts
    sudo dnf install google-droid-sans-mono-fonts
    sudo dnf install dejavu-sans-mono-fonts
    sudo dnf instakk google-noto-emoji-fonts
    sudo dnf install google-noto-emoji-fonts
    sudo dnf install google-noto-emoji-color-fonts

 To handle the bar at the bottom, i wrote this little configuration file. (another solution is to use polybar)

    general {
            colors = true
            interval = 5
         separator = "|"
    }
    
    
    order += "cpu_temperature 0"
    order += "memory"
    order += "battery 1"
    order += "tztime Paris"
    
    tztime Paris {
            format = "%H:%M"
            timezone = "Europe/Paris"
    }
    
    battery 1 {
            format = "%status %percentage %remaining "
            format_down = "No battery"
            status_chr = "⚡ CHR"
            status_bat = "🔋 BAT"
            status_unk = "? UNK"
            status_full = "☻ FULL"
            path = "/sys/class/power_supply/BAT1/uevent"
            low_threshold = 10
    }
    
    
    cpu_temperature 0 {
     format = "T: %degrees °C"
            path = "/sys/devices/platform/coretemp.0/hwmon/hwmon6/temp1_input"
    }
    
    
    memory {
            format = "%used"
            threshold_degraded = "10%"
            format_degraded = "MEMORY: %free"
    }

last but not least, I replaced the infamous urxvt terminal with alacritty

    bindsym $mod+Return exec alacritty

### my feelings about i3

Funny enough, it was not the time passed on configuration that frustrated me because you can as a user spend as much time as configuring i3 that configuring plasma or gnome (maybe even less time because there are more features and options in plasma than in i3). The issue with i3 and with probably most tiling window manager is you **need** to do it as a certain extent to have a fonctionnal system.

Resourcewise, i3 is probably around 2 to 3 times less resource heavy than gnome-shell. This is great but as a matter of fact it will not change radically your experience with your computer, your probably going to move from around 800Mb to 400Mb and use 2 times less CPU power. Those resource savings sounds well but are just comparable to a browser opened with a few tabs (maybe one or two) and won't radically change your experience with your computer. If you are using a lightweight desktop environment like xfce of mate, you will gain almost nothing resourcewise. I think resources saving should not be what drives you to tiling window management.

i3 resource usage :

![i3 htop](https://raw.githubusercontent.com/lachhebo/lachhebo.github.io/screenshots/i3_htop.png)

gnome resource usage

![gnome-shell htop](https://raw.githubusercontent.com/lachhebo/lachhebo.github.io/screenshots/gnome_shell_htop.png)

Don't forget you loose many features and some of them being useful when switching to a tiling window manager :

- dynamical workspaces
- dynamical management of multiple monitors  
- notifications
- overview

Actually, I think i3 is just not as efficient as classic desktop environment when dealing with dynamical events, like every issue with linux, you may find a fix for each of those by tweaking your desktops and writing some scripts. But you will need to have a certain amount of programming skills and free time to do that.

Another solution I tried is to install a [gnome-extension](https://extensions.gnome.org/extension/1286/tilingnome/) to replicate the tiling management workflow and it worked surprisally well.

## Conclusion

Tiling window manager are really interesssing, especicaly If you use your computer with a fixed setup (fix number of monitors, monitor placement, wifi and bluetooth) and your don't mind your grandma being unable to use your computer, It's probably not the best solution for laptop, casual or lazy users.

As for myself, this week was really interesting and I will not uninstall i3 from my computer as I felt in love with the tiling workflow, using once again stacking window manager like gnome or plasma after using a tiling window manager felt a bit frustrating. **However**, I will not use i3 as my main window manager as for now and uses a gnome-extension to keep advanced features I consider important.
