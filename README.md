

# TWITTER SCRAPER CODE IN 2022
[![Twitter API v2](https://img.shields.io/endpoint?url=https%3A%2F%2Ftwbadges.glitch.me%2Fbadges%2Fv2)](https://developer.twitter.com/en/docs/twitter-api)
[![PyPI Version](https://img.shields.io/pypi/v/tweepy?label=PyPI)](https://pypi.org/project/tweepy/)


![icons8-twitter](https://user-images.githubusercontent.com/70821494/154971422-8b2a8894-da12-40c1-9bc3-07f24039045b.gif)


# Purpose
This script is to show in lines of code how to scrape tweets from Twitter's user. Ex: Tweets, likes, creation time, etc.

## Table of contents
* [Setup of the Jupyter Notebook](#Setup-of-the-Jupyter-Notebook)
    * [Install](#Install)
    * [Imports](#Imports)
    * [Downloads](#Downloads)
* [BODY](#Body)
* [Outputs](#Outputs)
    * [Most-recent tweets in the user's Timeline](#Most-recent-tweets-in-the-user's-Timeline)
    * [Most used words in the user's Tweets](#Most-used-words-in-the-user's-Tweets)
    * [Who and what other users are talking about a certain Topic or User](#Who-and-what-other-users-are-talking-about-a-certain-Topic-or-User)


# Setup of the Jupyter Notebook

Install
-------

 You must install 3 packages separately.
 
 Spacy:
 ```bash
pip install Spacy 
```

setuptools wheel:
 ```bash
pip install setuptools wheel
```
 Tweepy:
 ```bash
pip install Tweepy 
```

Imports
-------

```bash
import tweepy

import configparser

import pandas as pd

import re

import spacy

import nltk

import matplotlib.pyplot as plt; plt.rcdefaults()

import numpy as np

import matplotlib.pyplot as plt

import seaborn as sns

from spacy import displacy

from collections import Counter

import en_core_web_sm

from spacy.lang.en import English

from nltk.probability import FreqDist
```

Downloads
-------

```bash
!python -m spacy download en_core_web_lg
!python -m spacy download en_core_web_sm
```

# Implement Twitter Keys
