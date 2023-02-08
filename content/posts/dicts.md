---
title: "Dictionaries and frequency lists for SSM"
date: 2021-08-11T13:29:37+08:00
draft: false
tags: ['dictionary', 'ssmtool', 'resource', 'frequency']
---
*This page is will be updated to include new resources. If you have any,
please inform us on the Matrix chatroom, link on the sidebar.*

Support for local dictionaries such as StarDict, Migaku, and JSON has been
added to ssmtool in version 0.3. This means you can use them for offline use,
or if Wiktionary do not have good coverage for your language. 

Support for local frequency lists have been added in version 0.5. This
information is displayed on the LCD counter widget on the window which should
help you decide whether to add a card (you might want to prioritize adding a
note with a word at frequency rank 5000, rather than another one at 40000).

<!--more-->

Here are some dictionaries available online for download, collected in a
single page.

## StarDict
**Hu Zheng (StarDict author) personal website, over 100 dictionaries**

http://download.huzheng.org/

**Russian Wiktionary Exports (Multiple languages with definitions in Russian)**

http://libredict.org/en/
(Might have formatting issues)

**English Wiktionary Exports**

http://www.dictinfo.com/
(Disclaimer: Not tested by author)

**GTongue Dictionaries**

https://sites.google.com/site/gtonguedict/home/stardict-dictionaries
(Disclaimer: Not tested by author)

**Converted Apple Dictionaries, 41 dictionaries, some bilingual**

https://rutracker.org/forum/viewtopic.php?t=6093047 (Torrent)

https://mega.nz/folder/Ll0wxYqa#2YLA7IHZhRZEfGHyZNqGdw (MEGA)

**Wiktionary for eBook Readers, also available in StarDict**

https://github.com/BoboTiG/ebook-reader-dict

## Migaku
**Migaku Official MEGA Folder, 11 languages**

https://mega.nz/folder/eyYwyIgY#3q4XQ3BhdvkFg9KsPe5avw/folder/bz4ywa5A

**Converted Apple Dictionaries, 41 dictionaries, some bilingual (Torrent)**

https://rutracker.org/forum/viewtopic.php?t=6093047 (Torrent)

https://mega.nz/folder/Ll0wxYqa#2YLA7IHZhRZEfGHyZNqGdw (MEGA)

## Simple JSONs
**English Wiktionary for Russian words, ~400k entries**

https://freelanguagetools.org/wikt-kaikki-ru.json

This file is produced from 
[Kaikki's Wiktionary dumps](https://kaikki.org/dictionary/). It should produce
results very similar to using the default `Wiktionary (English)` option
without using the internet.  I may create similar files for other languages at
a later date and/or if there is a demand for it. If you need a such a file,
message me on the chatroom linked on the sidebar.

## Frequency lists

**Lemmatized frequency list for Russian based on Ruscorpora**

https://freelanguagetools.org/freq_ru.json

This file is produced from 
[Russian frequency dictionary](http://dict.ruslang.ru/) which in turn comes
from the [Russian National Corpus](https://ruscorpora.ru/). This file is
lemmatized, which means you should turn on the "Lemmatize before looking up
frequency" option in the configuration tool.

**Lemmatized frequency list for English based on COCA corpus**

https://freelanguagetools.org/freq_en.json

Remember to use the "Lemmatize before looking up" option for this list.

**Migaku's frequency lists**

https://mega.nz/folder/eyYwyIgY#3q4XQ3BhdvkFg9KsPe5avw/folder/bz4ywa5A

These lists are *not* lemmatized. I recommend not using them for highly
inflected languages, as the results may be inaccurate or many words may not be
on the list due to the language have more than 100,000 word-forms in common
use. Do not use the "Lemmatize before looking up frequency" option if you
decide to use one of these lists.


## Other formats
These *will not* work with ssmtool, but you can use them in other programs,
such as [GoldenDict](https://github.com/goldendict/goldendict), a powerful
dictionary app. Support for them may be added in the future in ssmtool.

### BGL (Babylon)
Google drive folder, a lot of dictionaries, but mostly only for English, some
of them technical.
[Google drive](https://drive.google.com/drive/u/0/folders/0BzrQwK2v03aKWjlsQ3NsaWJKalU?resourcekey=0-DtgqOJiVFSDI231ugoQgiQ)

### DSL (Lingvo)
Rutracker GoldenDict Dictionaries (Russian, English, Ukrainian)
https://rutracker.org/forum/viewtopic.php?t=3369767
(Page in Russian, click "скачать" to download torrent)

## Conversion programs
You may be able to use these programs to convert your dictionaries in other
formats to a format supported by ssmtool:
https://github.com/ilius/pyglossary/tree/master/pyglossary

Unfortunately this might be difficult to install for Windows users. You're
welcome to ask for help on Matrix for conversion.
