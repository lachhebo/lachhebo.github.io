---
layout: post
title: 'GabTag, an audio tagging tool'
date: 2019-05-15
published: true
---

GabTag is a Linux audio tagging tool written in GTK 3, which makes it very suitable for GTK based desktop users. It is also the first Linux application I wrote.

The program allows users to select several files and modify their tags. It's also possible to let GabTag automatically find tags and lyrics for an audio file using MusicBrainz and lyrics.wikia.com database.

<a href='https://flathub.org/apps/details/com.github.lachhebo.Gabtag'><img width='240' alt='Download on Flathub' src='https://flathub.org/assets/badges/flathub-badge-en.png'/></a>

### Screenshots

<img height="350" src="https://raw.githubusercontent.com/lachhebo/GabTag/screenshots/Gabtag_v13_2.png" />

### Features

Some features have been developped but the application can still be improved.

- [x] Add, modify or delete basic tags (title, album, artist, genre)
- [x] other strings tags and labels
- [x] Cover tag
- [x] Modify several files at the same time.
- [x] MP3 File handled
- [ ] Flac File handled
- [x] bold font on modified tags and files
- [x] Automatic completion of tags (from online data)
- [x] Lyrics (from online data)
- [ ] Multi-folder modification
- [ ] Acoustic ID integration

#### Issues encontered during development

The issues i enconutered are mostly caused by the lack of documentation regarding gtk3 software development.

##### 1) setting up Travis-ci

The hardest thing for me has been to set up Travis-ci, I first set up a Travis-org ci (a deprecated version of Travis-ci) instead of the classic Travis-ci. Hence, I was not able to transfer my project in the newer version of Travis-CI. Then, I had to create a new GitHub repository to fix that. Eventually, I also struglled to find out that Travis need the python3-gi package and the PygObject pip package to be able to test the project.

##### 2) make the grid box scrollable

The second issue I encountered was linked to the layout. To make my grid layout scrollable, I had to put it inside a GtkAspectFrame and a GtkViewport. Anyway my layout is still not completely satisfying because i always need to resize the size of my panel when I'm using Gabtag.

##### 3) using GdkPixbufProlog

Last but not least, this issue which is still not fixed is with gdkpixbuf class. It is a bit surprising how showing an image can be hard in gtk. I had to use an external API called Pillow to show a byte image.

Even more surprising, for some image, the gtk pixbuf is not showing a scaled version of it but a deformed version of it. This issue is only apparing on my application so I hope I will be able to quickly fix it.

If you get a solution for those issues, you can send my an email to ismael.lachheb@protonmail.com. Otherwise, I hope my experience can help you.

#### Gathered skills

I am proud of my work and hope to keep improving Gabtag. This experience sharped my skills in :

- Python Development
- Continious Integration
- Object oriented programming
- Translation
- Flatpak packaging
- Reverse engineering
- Git
