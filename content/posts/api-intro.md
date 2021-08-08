---
title: "Announcing ssmtool local API"
date: 2021-08-08T17:34:53+08:00
draft: false
---
A basic but fully functional API has been added in `ssmtool` version 0.3. The
goal of this is to enable extensions for other programs, such as ebook readers
or video players, to depend on ssmtool's infrastructure and configuration. 

For developers, this can greatly reduce the workload since there is no longer
a need to program dictionary processing or lemmatization functions. For users,
they will only need to configure one tool rather than 3. Moreover, features
that would otherwise be absent for many simpler plugins such as lemmatization
will be available.

The current API only provides the features already in ssmtool, but in the
future the plan is to add features such as images and audio primarily in the
API, since ssmtool is mainly a text-oriented tool. 

Here is a table for the current API endpoints for reference.

| Verb | Path | Usage |
-------|-------|--------
GET | `/healthcheck` | Check if API is online
GET | `/version`| Get the version of API running. The current version is 1, which is the only possible value now.
GET | `/define/<word>` | Get the definition of a word. The response is a [definition item](#definition). Lemmatization depends on user setting.
GET | `/define/<word>?lemmatize=false` | Get the definition of a word regardless of user settings without lemmatization.
GET | `/lemmatize` | Get the lemmatized form of a word. Response is a simple string.
GET | `/logs` | Get the full database containing all past lookups and note creations
GET | `/stats` | Get data about lookups and new cards today
POST | `/createNote` | The request body should be a [note item](#note).

## Data formats
### Definition item
Depending on whether the user has a second dictionary source enabled, it can be either:
```json
{
    "word": "blue",
    "definition": "a color..."
}
```
or
```json
{
    "word": "blue",
    "definition": "a color...",
    "definition2": "azúl"
}
```
### Note item
```json
{
    "sentence": "The quick brown fox jumps over the lazy dog.",
    "word": "fox",
    "definition": "an animal..",
    "tags": []
}
```
Please note that even with "tags" being an empty array, the default tags
specified in ssmtool config will still be added.

Using two definitions is not yet supported. It should be added soon, along
with an interface to determine user settings since not all users will have a
second definition field set.

Image and audio data fields will also be added in the future.

## API users
Currently the author of mpv
[immersive](https://github.com/Ben-Kerman/immersive) script has plans to
support the API, at least as a dictionary function, which will transparently
provide lemmatization and handling of accents and other textual features in
different languages. 
