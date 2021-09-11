---
title: "Anki Decks from Tatoeba Sentences"
date: 2021-09-09T17:20:26-04:00
draft: true
tags: ['anki', 'tatoeba', 'resource', 'russian', 'programming']
---
This blog post is a tutorial on creating a CSV file to import into Anki using
Tatoeba sentences, a frequency list, and pre-downloaded Wiktionary entries.
You can find the frequency dictionary file (freqdict.csv) [here](/freqdict.csv).
You can download the Tatoeba sentences straight from 
[their website](https://tatoeba.org/en/downloads).

Even though this tutorial is specifically aimed at Russian, you can easily
adapt it to any other language with sufficient Tatoeba sentences, or any
bilingual dataset of sufficient quality.

If you need any help in adapting this to your language pair, ask us on the
Matrix chatroom linked on the side bar.

## Formatting explanation
```python
Code looks like this
```

    Output looks like this. (Tables are hand-formatted specially)

Note: Progress bars don't display properly here, so they show as 0% even
though they are all complete.

Note 2: The definition section in tables should be in HTML, but it is not
displayed here.

## Import common libraries
We are disabling warnings so that `pandas` would not complain about using slice
operators (the warned problem do not pose an issue to this use case, and
fixing them will make code more verbose)
```python
import warnings
warnings.filterwarnings("ignore")
import pandas as pd
import pymorphy2
from tqdm.notebook import tqdm
tqdm.pandas()
```

## Lemmatization setup
Here we are using PyMorphy2, which works for Russian and experimentally Ukrainian.
For other languages, you can look into [SpaCy](https://spacy.io/).
If your language does not have inflection, simply replace the code under the function `lem_text` with `return text.split()`


```python
morph = pymorphy2.MorphAnalyzer(lang="ru")
def lemmatize(word):
    "Lemmatize a word"
    return morph.parse(word)[0].normal_form

def lem_text(text):
    "Lemmatize a sentence and return a list"
    return [lemmatize(word) for word in text.split() if word]

lem_text("Я продолжаю получать спам по электронной почте.")
```




    ['я', 'продолжать', 'получать', 'спам', 'по', 'электронный', 'почте.']



## Load CSV file from Tatoeba
__IMPORTANT__: You need to check if they are in the right order. You may have to swap the order of "en" and "tl" tags.


```python
d = pd.read_csv('../langdata/sentences/en_ru.tsv', sep='\t', header=None, names=['id1', 'ru', 'id2', 'en'])
```


```python
d = d[['ru', 'en']]
```


```python
sample = d.sample(1000)
# Make sure this looks right. If not, swap the order in the second last
# cell, be sure to leave the double brackets as is.
print(sample.head(5).to_markdown())
```

|        | ru                                                      | en                                       |
|-------:|:--------------------------------------------------------|:-----------------------------------------|
| 327924 | Тебе не нужно извиняться перед Томом.                   | You don't need to apologize to Tom.      |
| 481741 | Есть ли у тебя вспышка, которую ты можешь мне одолжить? | Do you have a flashlight I could borrow? |
| 564452 | Том не может это есть.                                  | Tom can't eat that.                      |
| 289114 | Она умерла в своей постели в возрасте 96 лет.           | She died in her bed at the age of 96.    |
| 192477 | Три в кубе будет двадцать семь.                         | Three cubed is twenty-seven.             |



```python
def remove_punctuations(l):
    return [item for item in l if item.isalpha()]
```


```python
def getword(freq):
    return fl.loc[freq]['Lemma']
```

## Reading the frequency dictionary
This must be processed and be fully lemmatized, or else the result might be poor.

This list must not contain any duplicates.

Note that the definition column is in HTML, but they cannot be displayed here.


```python
fd = pd.read_csv("freqdict.csv", index_col="Unnamed: 0")[:20000]
fd2 = fd.reset_index().set_index("Lemma")
# Make sure this looks right
print(fd2.sample(10).to_markdown())
```

| Lemma             |   index | definition                                                                                                                                                  |
|:------------------|--------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| булыжник          |   12817 | <i>Noun</i><br>1. cobble, cobblestone                                                                                                                       |
| легонько          |   12925 | <i>Adverb</i><br>1. lightly<br>2. easily, facilely, slightly<br>3. luckily<br><i>Adjective</i><br>1. lightly<br>2. easily, facilely, slightly<br>3. luckily |
| акционер          |    3059 | <i>Noun</i><br>1. shareholder (one who owns shares of stock)                                                                                                |
| заведомо          |    7356 | <i>Adverb</i><br>1. deliberately, intentionally, knowingly<br>2. obviously                                                                                  |
| неуловимый        |   10027 | <i>Adjective</i><br>1. elusive, difficult to catch<br>2. imperceptible, subtle                                                                              |
| напасть           |   15351 | <i>Noun</i><br>1. misfortune, bad luck, trouble<br><i>Verb</i><br>1. misfortune, bad luck, trouble                                                          |
| погибший          |    7044 | <i>Verb</i><br>1. to perish, to die of unnatural causes, to be killed                                                                                       |
| накинуть          |    8507 | <i>Verb</i><br>1. to throw on, to throw over<br>2. to add                                                                                                   |
| привлекательность |    9626 | <i>Noun</i><br>1. attractiveness, appeal                                                                                                                    |
| столовый          |    6111 | <i>Adjective</i><br>1. table<br>2. dinner                                                                                                                   |


## Dictionary lookup function
We are using a pre-downloaded version of formatted English Wiktionary entries.

You can also use other dictionary formats, like a plain json or another CSV. If you choose to do so, you must reimplement the function below. The return value should be a string, either plaintext or with HTML tags.


```python
def get_def(word):
    try:
        return fd2.loc[word]['definition']
    except Exception:
        return None
get_def("накинуть")
```




    '<i>Verb</i><br>1. to throw on, to throw over<br>2. to add'


## Coverage testing functions
The first function tests the overall coverage, i.e. how much of the vocabulary
does the entire set of sentences cover. The second function tests word
coverage, i.e., how many words have their own cards. 

The overall coverage is displayed as a percentage of the frequency list up to
the specific level, whereas the word coverage is displayed as a raw number of
words.

```python
def test_coverage(data, upto=2000, downto=200):
    vocab = set.union(*data['lemmas'].apply(set).tolist())
    words = set(fl.iloc[downto:upto]['Lemma'])
    inter = vocab.intersection(words)
    covered_ratio = len(inter) / (upto - downto)
    return covered_ratio
```


```python
def test_word_coverage(data, upto=2000, downto=200):
    vocab = set(data[data.difficulty < upto][data.difficulty > downto]['target'].tolist())
    words = set(fl['Lemma'])
    inter = vocab.intersection(words)
    return len(inter)
```

```python
def test_cov_levels(data):
    a = [2000, 5000, 10000, 15000]
    b = [format(100 * test_coverage(data, level), "2.1f") + "%" for level in a]
    c = [format(test_word_coverage(data, level)) for level in a]
    return pd.DataFrame({"Level": a, "Words": c, "Coverage%": b}).set_index("Level")
```

## Getting missing words
```python
def get_missings(data, upto=5000, downto=200):
    vocab = set.union(*data['lemmas'].apply(set).tolist())
    words = set(fl.iloc[downto:upto]['Lemma'])
    inter = vocab.intersection(words)
    return words - inter
```


```python
def format_lemmas(lemmas):
    return " · ".join(lemmas)
```

## Sentence difficulty function
This function takes a list of words and returns the index of the word ranked
the highest on the frequency list ("the hardest word")

This ideally would guarantee that you would never study a word before you know
all the other ones, but in practice does not work perfectly, though you should
still have single-unknown sentences for the most part if you study them in
order.

```python
def get_dif(l):
    if len(res:=fl2.reindex(l)['index'].fillna(0)) != 0:
        return int(max(res))
    else:
        return 0
```

## Processing function
This does the first two steps, which are lemmatization and calculating
difficulty.

```python
def process_sentences(data):
    print("STEP 1: Lemmatization")
    data.loc[:, "lemmas"] = data['ru'].progress_apply(lem_text)
    data.loc[:, 'lemmas'] = data['lemmas'].apply(remove_punctuations)
    print("STEP 2: Calculating frequency scores")
    data.loc[:, 'difficulty'] = data['lemmas'].progress_apply(get_dif)
    data.loc[:, 'lemmas_formatted'] = data['lemmas'].apply(format_lemmas)
    data = data[data['difficulty'] < 15000]
    return data.sort_values('difficulty')
```

## Sentence complement
The downside of taking sentences solely by the most difficult word is that it
will miss a lot of useful sentences, especially those with an unknown word,
but with a more difficult word somewhere in it.

We first deduplicate the dataset, so that each word only has one sentence for
it. Then, for each missing word, we try to find the easiest sentence that
contains it, and we modify the difficulty of that sentence by +0.5 so that it
will be studied after the sentence that targets the highest-ranked word is
studied, ensuring as many cards as possible are single-unknown. We add these
sentences back to the list. 
```python
def get_complemented(processed):
    """
    First deduplicate the sentences, and then add sentences back to enhance the range
    The easiest sentence that has a missing word is picked, and it's difficulty is 0.5 plus the difficulty of that word
    so that it will be studied only after the highest ranked word is already studied.
    """
    print("STEP 4: Deduplication")
    print("  Size of processed data: ", len(processed))
    norepeat = processed.drop_duplicates("difficulty")
    print("  Size of deduplicated data: ", len(norepeat))
    print("  Coverage of deduplicated data:")
    print(test_cov_levels(norepeat).to_markdown())
    missings = get_missings(norepeat) - get_missings(processed)
    result = pd.DataFrame()
    print("STEP 5: Finding complement")
    for word in missings:
        row = processed[processed.lemmas_formatted.str.contains(word)].reset_index(drop=True).reindex([0]).loc[0]
        row['target'] = word
        row['difficulty'] = row['difficulty'] + 0.5
        result = result.append(row)
    result = result[["en", "ru", "lemmas", "difficulty", "lemmas_formatted", "target"]]
    complement = result.dropna()
    enhanced = norepeat.append(complement)
    print("\tSize of enhanced data: ", len(enhanced))
    return enhanced.sort_values('difficulty').reset_index(drop=True)
```


```python
def add_targets(data):
    print("STEP 3: Add targets to sentences")
    data = data[data.difficulty > 200]
    data['target'] = data["difficulty"].apply(getword)
    return data
```


```python
def lookup_defs(data):
    print("STEP 6: Look up definitions")
    data.loc[:, "definition"] = data.target.progress_apply(get_def)
    return data
```


```python
def full_processing(data):
    output = process_sentences(data)
    output = add_targets(output)
    print(test_cov_levels(output).to_markdown())
    output = get_complemented(output)
    print(test_cov_levels(output).to_markdown())
    output = lookup_defs(output)
    n_def = len(output.definition.notna())
    print(n_def, " definitions found.")
    output = output.drop("lemmas", axis=1)
    return output
```

## Processing
Now all the relevant functions have been defined. We can start with a small sample to check for errors before running it on the full list.


```python
#Calculate a sample first to check for errors. If this runs successfully, you may use the full list.
sample = d.sample(100000)
sm = full_processing(sample)
```

    STEP 1: Lemmatization



      0%|          | 0/100000 [00:00<?, ?it/s]


    STEP 2: Calculating frequency scores



      0%|          | 0/100000 [00:00<?, ?it/s]


    STEP 3: Add targets to sentences

|   Level |   Words | Coverage%   |
|--------:|--------:|:------------|
|    2000 |    1339 | 85.5%       |
|    5000 |    3090 | 73.7%       |
|   10000 |    4824 | 55.3%       |
|   15000 |    5871 | 43.8%       |

    STEP 4: Deduplication
      Size of processed data:  62499
      Size of deduplicated data:  5871
      Coverage of deduplicated data:

|   Level |   Words | Coverage%   |
|--------:|--------:|:------------|
|    2000 |    1339 | 81.4%       |
|    5000 |    3090 | 69.9%       |
|   10000 |    4824 | 52.8%       |
|   15000 |    5871 | 42.2%       |

    STEP 5: Finding complement
    	Size of enhanced data:  6054

|   Level |   Words | Coverage%   |
|--------:|--------:|:------------|
|    2000 |    1373 | 85.2%       |
|    5000 |    3186 | 73.3%       |
|   10000 |    4989 | 54.6%       |
|   15000 |    6054 | 43.3%       |

    STEP 6: Look up definitions



      0%|          | 0/6054 [00:00<?, ?it/s]


    6054  definitions found.
```python
print(sm.head(5).to_markdown())
```

|    | ru                                  | en                              |   difficulty | lemmas_formatted                   | target      | definition                                                                                                      |
|---:|:------------------------------------|:--------------------------------|-------------:|:-----------------------------------|:------------|:----------------------------------------------------------------------------------------------------------------|
|  0 | Я дал Тому возможность это сделать. | I gave Tom a chance to do that. |          201 | я · дать · тот · возможность · это | возможность | <i>Noun</i><br>1. opportunity, chance, potential (chance for advancement, progress or profit)<br>2. possibility |
|  1 | Каких результатов ты ждёшь?         | What results do you anticipate? |          202 | какой · результат · ты             | результат   | <i>Noun</i><br>1. effect, result, return, outcome                                                               |
|  2 | Ночь была холодной.                 | It was a cold night.            |          203 | ночь · быть                        | ночь        | <i>Noun</i><br>1. night                                                                                         |
|  3 | Стол в комнате.                     | The table is in the room.       |          204 | стол · в                           | стол        | <i>Noun</i><br>1. table<br>2. board, fare, cuisine<br>3. department, section, office, bureau<br>4. throne       |
|  4 | Ты никогда её не найдёшь.           | You'll never find her.          |          205 | ты · никогда · её · не             | никогда     | <i>Adverb</i><br>1. never, nevermore (entails the meaning "always" or "for now on")                             |

## Full processing
This will take quite some time, depending on the power of your computer.
If you have a much bigger database, you might want to consider using
multiprocessing for the `get_dif` and `lemmatize` functions. The library
`pandarallel` is a good choice for this.
```python
full = full_processing(d)
full.to_csv("output.csv")
```


