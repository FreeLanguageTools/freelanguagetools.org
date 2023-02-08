---
title: "Updating to ru15k v3.0"
date: 2022-06-15T00:00:00-04:00
tags: ["anki", "russian", "ru15k", "tutorial"]
draft: false
---
The new version (v3.0) of the ru15k deck has just been
[released](https://ankiweb.net/shared/info/563580199). This post contains
instructions for existing users of the earlier versions of ru15k who wants to
update to the new version. If you are a new user, or only studied a small
number of cards from the original ru15k, you can also simply delete the
original deck and start using this deck directly, which would not require any
manual intervention. If you have done an upgrade before, the process should be
largely the same.

<!--more-->

Differences from the old version:
 - Bolded targets word for quicker reviews
 - First 2000 cards are now manually reviewed (not including the lemmas). They should be generally free of errors in terms of the sentence and definitions, as well as word stress
 - Stress marks and ё on (mostly) all words
 - Yandex audio pronunciation is now used instead of Google

Before taking any action, please:
- *Make a full backup of your collection* (click on any deck -> export -> Anki
  Collection Package (tick Include media))
- Read this article in full

**I am in no way responsible for the loss of your data.**

## Updating the deck
Download the new deck from [AnkiWeb](https://ankiweb.net/shared/info/563580199)
1. Rename the original deck back to "ru15k". It cannot be a subdeck. This is needed for the new cards to move to the correct deck automatically.
2. Import the file for the new deck

## Fixing card ordering
The new deck has different index-word correspondences from the original one, especially from the original ru15k deck. This means after you import the deck, the queue of your new cards will be somewhat scrambled. This is not necessarily a big problem, but it can cause you to miss more words than you need to on the new deck.
To fix this, do the following:

1. Open deck browser, select the ru15k deck
2. Choose "cards" view
3. Sort it by clicking on the "Sort field" button. Make sure the row on the top is "100.0"
4. Select all, right click -> Reposition
5. Check "Shift position of existing cards". Leave start position as 0 and step as 1, then click OK.


If you missed any of these steps, you should restore your backup and start over. Do not import it twice, since that can lead to strange effects.

You can then resume studying. If you are an existing user of the original deck, you will likely have to suspend through many early cards, but you should notice that the rank of the new cards are always increasing rather than moving up and down.

If you encounter any issues, please join our Matrix chatroom on the sidebar,
where you can ask questions.

## Delete leftover media
After importing the deck, you can remove the now unused media from previous versions by clicking "Tools->Check Media->Delete Unused" and then again "Tools->Check Media->Empty Trash." This way, you'll spare about 200 MB of space.

## Delete leftover cards
Some cards, such as the one with word fields using the letter е instead of ё
are deprecated. There will be a message asking you to delete them. There are
not many of them, and you can simply delete them with Ctrl-Delete during
review.

