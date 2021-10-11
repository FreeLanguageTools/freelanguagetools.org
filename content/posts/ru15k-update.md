---
title: "Updating to ru15k v2.0"
date: 2021-10-10T11:54:08-04:00
tags: ["anki", "russian", "ru15k", "tutorial"]
draft: false
---
The new version of the ru15k deck has just been released. This post contains instructions for existing users of the original ru15k who wants to update to the new version. If you are a new user, or only studied a small number of cards from the original ru15k, you can also simply delete the original deck and start using this deck directly, which would not require any manual intervention.

<!--more-->

Differences from the old version:
- Covers much more words - over 95% of the words up to level 15000
- Greatly reduced lemmatization errors thanks to PyMorphy2
- Wiktionary definitions, which are in more detail than the previous one
- Monolingual sentences after rank 5000
- Manually checked up to rank 1000

Before taking any action, please:
- *Make a full backup of your collection* (click on any deck -> export -> Anki Collection Package (tick Include media))
- Read this article in full

**I am in no way responsible for the loss of your data.**

## Updating the deck
1. Rename the original deck back to "ru15k". It cannot be a subdeck. This is needed for the new cards to move to the correct deck automatically.
2. Import the file for the new deck

## Fixing card ordering
The new deck has different index-word correspondences from the original one. This means after you import the deck, the queue of your new cards will be somewhat scrambled. This is not necessarily a big problem, but it can cause you to miss more words than you need to on the new deck.
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
