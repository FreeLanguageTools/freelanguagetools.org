---
title: "Hello World"
date: 2021-07-28T13:06:49+08:00
draft: false
---
Hello, this is the beginning of the FreeLanguageTools.org website. On this website
I will be writing about the tools for learning languages without sacrificing
your freedom (such as by using proprietary apps)

A while ago, I came across [Refold](https://refold.la), which was by far the
clearest and most promising path to fluency I had seen, and matches up well
with my experience of learning English. I decided to use it for learning
Russian partly as an experiment.

As I attempted to immerse in content, I wanted a way to easily create
flashcards from sentences I encounter in the wild. However, everything I found
seems to had downsides. Common one include:
- Proprietary (Readlang, LinQ, Migaku), some of which being actually fairly expensive.
- No Anki integration (Having to use their crappy online flashcard services
  unless I was willing to export things regularly, which sounded like a hassle)
- Dependence on Google Translate, which often don't give full or even remotely
  detailed definitions suitable for flashcards

For this reason, I created
[ssmtool](https://github.com/FreeLanguageTools/ssmtool), which is a 
[free software](https://www.gnu.org/philosophy/free-sw.html) based solution to 
all this. It leverages Wiktionary and other APIs to obtain definitions and uses 
AnkiConnect to create cards directly, without using exports.

Here are some of its features:
- It supports both Monolingual (Google dictionary) and Bilingual (Wiktionary
  or Google translate) definitions [^1]
- Cross platform: It supports GNU/Linux, Windows, and macOS

And most importantly of all:
- It's truly yours: no EULA, no Terms and Conditions, no tracking

In the future, some more features might be added to ssmtool, and I might
create more integrations for it for video players. The final goal is to build
a complete set of free software tools for immersion based language learning.

[^1]: This depends on the target language, the full language support details
  can be seen from the source code or another blog post here at a later date.
