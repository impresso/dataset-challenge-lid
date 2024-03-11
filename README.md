# Challenging Language Identification Data Set for impresso languages
This repository contains human-validated text snippets from the impresso dataset.
The data can be used to evaluate language identification models on OCR noisy data.
It has also been used to train and evaluate language identification models for the
impresso project. 

## Data set
See exploration.ipynb for an interactive exploration of the data set.
Currently, we have the following (skewed) distribution of human-validated labels:

```
[de]                2874
[fr]                1615
[lb]                 822
[de, fr]             269
[en]                 168
[it]                 140
[fr, lb]              87
[de, lb]              70
[la]                   7
[de, la]               7
[en, fr]               5
[de, fr, lb]           4
[en, lb]               4
[en, fr, lb]           3
[de, en, fr]           3
[de, en]               2
[de, fr, it]           2
[de, en, lb]           1
[nl]                   1
[de, it]               1
[de, fr, la]           1
[fr, it]               1
[de, fr, la, lb]       1
```

### Data format
JSONL has the following fields:
  - `id`: the impresso id of the article
  - `text`: The raw text snippet. The length of the snippet is not fixed, but not longer
    than 1200 characters (including spaces). For human validation, we sometimes onl kept
    the first 400 and the last 400 characters. These items have 5 white-space characters
    where the split happened.
  - `langs`: The languages of the text snippet as a list of two-letter language codes in
    alphabetical order.
  - `length`: The length of the text snippet in characters (including the 5 white-space 
    characters). This is a redundant field, but it makes it easier to filter the data.
  - `annotation-source`: The internal information about the source. See below for some
    background information on the sampling process.
  - `impresso-url`: A link to the impresso viewer with the article. This is not a
    permalink, but mostly works. For some items the ids might have changed.

### Background information on sampling
The data set was sampled from the impresso dataset. The sampling was done by comparing
metadata from the archives with the output of language identification models (focusing
on mismatches), or by focusing on language identification model outputs that contradict
each other.

The following annotation-source labels have the following background:
  - "langid-luxemburgish-eval-{1,2,3}": Evaluation on cases where original language from archive has lb as language, but the
    language identification tool langid thinks it is another language.
  - "language-identification-evaluation-langdetect-1", "final2-impresso-lid-lg-it-or-la-evaluation":  Evaluation on cases where
    original language from archive is not lb and not null and langdetect does not equal
    it.
  

  
# License
The labels are licensed under the terms of the LICENSE file. The text snippets are
licensed under the terms of the impresso dataset license and restrictions might apply.
