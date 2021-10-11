---
title: "Using SSM with mpvacious to mine videos"
date: 2021-09-21T18:21:04-04:00
tags: ['tutorial', 'ssmtool', 'anki']
draft: false
---
[Mpvacious](https://github.com/Ajatt-Tools/mpvacious) is an addon
for the [mpv](https://github.com/Ajatt-Tools/mpvacious) video player. Mpv is a
[free](https://www.gnu.org/philosophy/free-sw.html), keyboard-driven and
highly extensible, which makes it particularly suitable for language learning.


Mpvacious facilitates making Anki notes from subtitled videos. While it
supports adding notes directly, in this post we will use SSM to actually add
the cards, then use mpvacious to add the screenshot and audio afterwards.

<!--more-->
## Prerequisites
You need a functional copy of ssmtool, Anki, and AnkiConnect running on your
computer. If you don't, you can refer to this
[post](/2021/07/simple-sentence-mining-ssmtool-full-tutorial/) for a guide to
set all of them up.

You also need to install mpv. On GNU/Linux, you should simply install it from
your distribution's repositories. On Windows and macOS, install it from the
links on the mpv [website](https://mpv.io/installation/).

## Installation of mpvacious
To install mpvacious, you should clone its
[repository](https://github.com/Ajatt-Tools/mpvacious). 

If you don't know how to do this, click on the green "Code" button and choose
"Download ZIP".

Either way, the contents of the repository should go to the following
directory.
- GNU/Linux: `~/.config/mpv/scripts/`
- Windows: `C:/Users/Username/AppData/Roaming/mpv/scripts/`

## Configuration
Open the following file, which may or may not already exist:
- GNU/Linux: `~/.config/mpv/script-opts/subs2srs.conf`
- Windows: `~/.config/mpv/script-opts/subs2srs.conf`

Then, paste in the content in this
[link](https://raw.githubusercontent.com/Ajatt-Tools/mpvacious/master/.github/RELEASE/subs2srs.conf).
You should edit the file according to your deck setup. Most of these options
do not have to be changed, but a few would be necessary for most people.

Pay attention to the following:
- `deck_name` Name of your deck
- `model_name` Name of your note type
- `audio_field` Name of the field to add audio to
- `image_field` Name of the field to add screenshot to
- `nuke_spaces` Set this to no if the language you study use spaces.
- `autoclip` Set this to yes so that the auto-copying feature is on by
  default 
- `snapshot_height` Change this if you want a bigger image

## Usage
![Screenshot of using mpvacious and SSM to add notes](/ssm-mpvacious.png)
Open any video with mpv. If you have set `autoclip` to `yes`, you can skip
this, but if not, you should press Ctrl-t to toggle the automatic copying
feature.

Then, open a window of ssmtool by the side, scale it to fit your need. You
should notice that each new subtitle appears on the top field of ssmtool.
Whenever there is a word you want to make a card for, pause the video and look
it up by double-clicking on the word.

After you're satisfied with the definition, press Add Note in ssmtool, and
switch back to mpv and press Ctrl-m to add screenshot and audio to the note
you just added. This should open a Anki Browser window, which you can use to
preview the new note.

This is all you need for now, if you have well-timed subtitles. Mpvacious
offers many more features, which you can read about
[here](https://github.com/Ajatt-Tools/mpvacious).

In the future, I might attempt to add features to further integrate ssmtool
and mpvacious, such as by transmitting the audio and screenshot to the
clipboard directly and avoid the need to update the note afterwards.
