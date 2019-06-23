---
title: "Development Journal : GabTag 1"
published: true
---

Here, I would like to present my experience making my first Linux Gtk application. I will mostly talk about the issues i encountered because it is the most interesseting part and the most informative too.

## Issues encontered

### First issue : Setting up Travis-ci

I think the hardest thing for me has been to set up Travis-ci, I first set up a Travis-org CI (a deprecated version of Travsi) instead of the classic Travis-ci and I was not able to transfer my project in the right version of travis. I had to create a new GitHub repository to fix that. Then when it was done, I had to guess that Travis need the python3-gi package and the PygObjext pip package to be able to test the project. It was hard to guess because I first tried to install all dependency using only apt and then only using pip but I needed to install those with both.

### Second issue : make a  grid scrollable 

The second i encountered was the layout, to make my grid layout scrollable, i had to put it inside a GtkAspectFrame and a GtkViewport which are not the easiest objects to access with glade. Anyway my layout is still not completely satisfying because i always need to resize the size of my panel when i'm using Gabtag.


### Third issue : Using GdkPixbuf

Finally the third issue which is still not fixed is with gdkpixbuf class. It is a bit surprising how printing an image can be hard in gtk. I had to use an external API called Pillow to show a byte image. 

Even more surprising, for some image, the gtk pixbuf is not showing a scaled version of it but a strange bruited image. This issue is only apparing on my application so I hope I will be able to quickly fix it. 


### Conclusion :

 If you get a solution for those issues, you can send my an email to ismael.lachheb@protonmail.com. Otherwise, i hope my experience can help you.
