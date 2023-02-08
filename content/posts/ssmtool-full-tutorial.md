---
title: "Simple Sentence Mining (ssmtool) full tutorial"
date: 2021-07-30T13:23:10+08:00
draft: false
tags: ['ssmtool', 'tutorial']
---
## Introduction
Simple Sentence Mining (ssmtool) is a universal, cross-platform, multilingual,
clipboard-based tool that helps you generate Anki flashcards from whatever
source. It is free software under the 
[GNU GPLv3](https://www.gnu.org/licenses/gpl-3.0.en.html) license, meaning you
are free to use, modify, and distribute it, even commerically, as long as it
remains under the same license.

<!--more-->

It is designed to be simple to set up and straightforward, with the ultimate
goal of enabling smooth sentence mining during immersion study. Originally, I
wanted to make an Anki add-on, however, I noticed several issues with that
idea:
- Anki has no stable API, and addons break regularly on every release, making
  it difficult to maintain.
- I would like the tool to be extensible for other, potentially better
  flashcard tools in the future.

## Feature set
### Easy word lookups
You can simply copy anything to the clipboard. If it is a single word, it will
be looked up right away, which allows you to use it as a dictionary app too.

Otherwise, when the copied content appears in the "Sentence" field, you can
simply double click it to look it up. For languages not using spaces, you will
have to select it manually, and then either press the button or use the
keyboard shortcut. Better support for Chinese and Japanese is expected in the
near future.

### Online and local dictionaries
From version 0.2.0 ssmtool comes with three dictionaries out of the box
- English Wiktionary `wikt-en` (Definitions are in English; support for other
  languages here depends on progress on their API)
- Google Translate `gtrans` (Translating to any other supported language)
- Google Dictionary `gdict` (Monolingual, i.e., definitions in the same
  language)[^1]

[^1]: The maintainer of the project has said that they would transition to
  English Wiktionary definitions due to copyright concerns. So far, this has
  not happened. In the event that it does, this option will be removed, as
  there is already an option for using English Wiktionary.

Local dictionaries (StarDicts, Migaku JSON files, and simple JSON key:value
pairs) are also supported. To find dictionaries, check
[this post](https://freelanguagetools.org/2021/08/dictionary-resources-for-ssmtool/).

### Frequency lists and pronunciations
SSM is able to import frequency lists in the format of a JSON array file, such
as the ones available on the MEGA folder linked in the post linked above.
If a frequency list is enabled, frequency rank for words will be displayed on
the main window to help you decide whether to add a note.

In addition, SSM can fetch native pronunciations from Forvo and export the
audio to Anki. 

### Lemmatization
Many similar tools such as LingQ, Readlang, and Learn with Texts do not have
the ability to lemmatize words, which is to convert words into their
dictionary forms. The issue with this is that many dictionaries do not have
all forms of a word listed, especially in highly inflectional languages
(Russian, Finnish).  With lemmatization, dictionary lookups become much
smoother because there is no longer a need to manually modify the word before
looking it up. 

### Anki integration
This program leverages AnkiConnect to add cards directly to Anki, without
using csv exports. Tags and custom note layouts are also supported. 

### Browser integration
The Click Copy Sentence extension is available for 
[Firefox](https://addons.mozilla.org/en-GB/firefox/addon/click-copy-sentence/) 
and
[Chrome](https://chrome.google.com/webstore/detail/click-copy-sentence/klhlkoabjmofmjkhbmelmfnhkbjaohdj) (incl. derivatives). 

This extension enables you to mine sentences with a single click on most
websites, further smoothening the immersion experience.

### Language Support Matrix
|Language|`lemma`|`wikt-en`|`gdict`|`gtrans`|"Support level"[^2]|
| ------ | ----------- | ------- | ----- | ------ | ---------------- |
| English | {{<check>}} | {{<check>}} | {{<check>}} | {{<check>}} | Full |
| Russian | {{<check>}} | {{<check>}} | {{<check>}} | {{<check>}} | Full |
| Chinese | | {{<check>}} | {{<check>}} | {{<check>}} | Partial |
| Italian | {{<check>}} | {{<check>}} | {{<check>}} | {{<check>}} | Full |
| Finnish | {{<check>}} | {{<check>}} | {{<check>}} | {{<check>}} | Partial |
| Japanese | | {{<check>}} | {{<check>}} | {{<check>}} | Partial |
| Spanish | {{<check>}} | {{<check>}} | {{<check>}} | {{<check>}} | Full |
| French | {{<check>}} | {{<check>}} | {{<check>}} | {{<check>}} | Full |
| German | {{<check>}} | {{<check>}} | {{<check>}} | {{<check>}} | Full |
| Latin | {{<check>}} | {{<check>}} | | {{<check>}} | Partial |
| Polish | | {{<check>}} | | {{<check>}} | Partial |
| Portuguese | {{<check>}} | {{<check>}} | {{<check>}}[^3] | {{<check>}} | Full | 
| Serbo-Croatian | | {{<check>}} | | {{<check>}} | Partial |
| Dutch | {{<check>}} | {{<check>}} | | {{<check>}} | Partial |
| Romanian | {{<check>}} | {{<check>}} | | {{<check>}} | Partial |
| Hindi | | {{<check>}} | {{<check>}} | {{<check>}} | Partial |
| Korean | | {{<check>}} | {{<check>}} | {{<check>}} | Partial |
| Arabic | | {{<check>}} | {{<check>}} | {{<check>}} | Partial |
| Turkish | {{<check>}} | {{<check>}} | {{<check>}} | {{<check>}} | Full |

[^2]: "Full support" simply means the full feature-set is available. Usability
  can depend on a lot of other factors, such as 
  [dictionary coverage](https://en.wiktionary.org/wiki/Wiktionary:Statistics) 
  and
  [lemmatizer accuracy](https://github.com/adbar/simplemma),
  both of which can vary depending on the language.
[^3]: Only the Brazillian variant. It will be selected automatically if Google
  dictionary is chosen

## Installation
There are three components you need to install to make this program work.

### Main Desktop Application
#### GNU/Linux
Gentoo: `app-misc/ssmtool::guru`

Arch Linux AUR: `ssmtool`

Otherwise, you can use `pip install ssmtool` (or pip3 if appropriate)
This will install a desktop file which you should be able to see from your
launcher menu. If you do not use a desktop environment, you can launch it
through the command line `ssmtool`.

On Linux the appearance of the app depends on the system Qt theme.

#### Windows and macOS
Even though we encourage the use of free software, nonfree operating systems
are still supported by this tool. You can go to the 
[Github Releases](https://github.com/FreeLanguageTools/ssmtool/releases) 
for standalone versions. 

If you are feeling brave, you are also welcome to go to
[AppVeyor](https://ci.appveyor.com/project/1over137/ssmtool) to obtain the
latest builds, but they are not guaranteed to run.

Alternatively, or if you would like a development version, you can also run
the same `pip` command above. 

Only 64 bit Windows 7+ is supported. On Windows you need the
[Microsoft Visual C++ Redistributable Package](https://aka.ms/vs/16/release/vc_redist.x64.exe),
which you may or may not already have.

Since I do not have a Mac computer now, the macOS builds are not tested. If
you use a Mac and found that it does not work, please report to Github or our
chatroom. If you are interested you can also help test future versions.

### Anki Add-on (Required for card creation)
Download and install [Anki dekstop](https://apps.ankiweb.net/) (Not mobile or Anki Universal). Skip if you already installed it.

Then, install the [AnkiConnect](https://ankiweb.net/shared/info/2055492159)
addon. You do not have to change any settings for it.

**Mac users**: You must have Anki open on the foreground (i.e. visible on your
desktop), or otherwise 
[disable the App Nap feature](https://github.com/FooSoft/anki-connect#notes-for-macos-users).
If you do not do this, AnkiConnect will not respond and will cause this
program to be very slow and/or unresponsive.

### Browser (Optional but highly recommended)
Install extension for your browser:
- [Firefox](https://addons.mozilla.org/en-GB/firefox/addon/click-copy-sentence/)
- [Chrome](https://chrome.google.com/webstore/detail/click-copy-sentence/klhlkoabjmofmjkhbmelmfnhkbjaohdj) (incl. derivatives such as Edge, Brave, etc.) 

Alternatively, if you have articles or books to read, you can also use
the HTML [reader app](https://freelanguagetools.org/apps/reader/), which does
not require using the browser extension.

## Configuration
You need to first select a target language from the list. Then, you can select
a dictionary. We recommend using Google translation only if the other two are
not available, because translations are always less detailed than dictionary
definitions and may not provide the full range of meanings needed.

We recommend leaving lemmatization on as it is by default. It can greatly
boost dictionary coverage for many languages. 

Optionally, you can add frequency lists and local dictionary files via the
bottom option of "Manage local dictionaries". Consult 
[this post](https://freelanguagetools.org/2021/08/dictionaries-and-frequency-lists-for-ssm/)
for compatible files.

Next, on the Anki tab, you will see a number of settings. You usually do not
have to change the first one, which is the API endpoint, unless you configured
a different endpoint in AnkiConnect, but in that case you will know how to do
this. You should then select a deck, note type, and match data fields into
note fields. To do this you must have a note type with at least three fields,
one each for Sentence, Word, and Definition. 

If you do not have one, you can download it from
[here](https://freelanguagetools.org/sample.apkg) and import it into Anki.
Then, select "ssmtool-reading" and simply match the field names.

You're done! Now you are ready to mine sentences.

## Usage
### General
When you see any sentence from anywhere, you can simply copy it to clipboard.
It will appear on the Sentence field right away. Then, double click on any
word, and you will get the definition. You can look up words from the
Definition field too. Then, when you are satisfied with the data, click on Add
Note to send it to Anki.

**Note**: It seems that on macOS clipboard change may not always be detected.
In that case simply use the "Read clipboard" button.

### Browser
When you turn on the extension, you will notice that sentences are underlined
in green (will become configurable in the future). Whenever you click on any
word, ssmtool will receive both the whole sentence and the word under your
cursor. The word will be looked up immediately too. Chances are, with
lemmatization on, this is exactly the word you want. In that case, just press
Ctrl/Cmd + S, and you can keep reading!

### mpv
You can use this tool in combination with [mpv](https://mpv.io) with the
[mpvacious plugin](https://github.com/Ajatt-Tools/mpvacious) to make it copy
subtitles to clipboard continuously. Audio data is currently not supported,
but may be added in the near future either as an extension to ssmtool, or as a
standalone mpv plugin.

### AwesomeTTS
Currently ssmtool does not support directly adding audio during card creation.
However you can easily get the audio during review with 
[AwesomeTTS Anki addon](https://ankiweb.net/shared/info/814349176).
After [configuring](https://github.com/AwesomeTTS/awesometts-anki-addon/wiki/Advanced)
it, you can go to 
`Tools > Manage Note Types > (select your note type) > Cards > Add TTS`
Then, select the Sentence field, the Word field, or both. Refold recommends
putting audio on the back of the card, but it is also possible to put it on
the front side.

## Feedback
You are welcome to report bugs, suggest features/enhancements, or ask for
clarifications by 
[opening a GitHub issue](https://github.com/FreeLanguageTools/ssmtool/issues/new).

We have an official chatroom on [Matrix](https://matrix.to/#/#flt:matrix.org)
and on [Telegram](https://t.me/fltchat).

You are also welcome ask _z#6358 on Refold Discord for help.
