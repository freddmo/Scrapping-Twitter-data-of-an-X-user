

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


## Setup of the Jupyter Notebook

### Install

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

### Imports

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

### Downloads

```bash
!python -m spacy download en_core_web_lg
!python -m spacy download en_core_web_sm
```

## Implementation of Twitter Keys

Texto
```bash
config = configparser.ConfigParser()

config.read('config.ini')
```

Set the respectives keys
```bash
api_key = config['twitter']['api_key']
api_key_secret = config['twitter']['api_key_secret']
access_token = config['twitter']['access_token']
access_token_secret = config['twitter']['access_token_secret']
```

Set the API
```bash
auth = tweepy.OAuthHandler(api_key, api_key_secret)

auth.set_access_token(access_token, access_token_secret)

api = tweepy.API(auth)
```

### Who we will use as an example? Elon Musk
```bash
limit = 200

elon_tweets = tweepy.Cursor(api.user_timeline, id='elonmusk', tweet_mode ='extended').items(limit)

elon_tweets_list = [[tweet.created_at,tweet.favorite_count, tweet.full_text] for tweet in elon_tweets]


columns = ['Time','Likes','Tweet']

df_ET = pd.DataFrame(elon_tweets_list, columns=columns)  # df_Elon_tweets

df_ET
```

### Further analisis of Elon's Tweet
```bash
limit = 200

E_tweets = tweepy.Cursor(api.user_timeline, id='elonmusk',
                           count=100, tweet_mode ='extended').items(limit)

elon_data = []

for tweet in E_tweets:
    elon_data.append(tweet.full_text)
   
    
elon_data
``` 
### Pre-process the data

Now that we have all sentences separated we repeat the process to get every word.
```bash
Sentences = []

for word in elon_data:
    Sentences.append(word)
    
lines = list()

for line in Sentences:
    words = line.split()
    
    for w in words:
        lines.append(w)
        
print(lines)
``` 

To eliminate all characters thata weren't in the alphabet I used the 
```bash
lines_V2 = [re.sub(r'[^A-Za-z0-9]+', '', x) for x in lines]  #lines_version_2

lines_V3 = []

for word in lines_V2:
    if word != 'RT' and word != '' and word != 'I':
        lines_V3.append(word)


nlp = spacy.load('en_core_web_lg')

lines_V4 = []

for word in lines_V3:
    if word not in nlp.Defaults.stop_words:
        lines_V4.append(word)

lines_V4
``` 
## OUTPUTS

### Most-recent tweets in the user's Timeline


Date and Time Created      | Likes         | Tweet
-------------------------- | ------------- | -------------
2022-02-20 22:25:19+00:00  | 17025         | @TPostMillennial Hypocritical megadouche!
2022-02-20 22:24:03+00:00  | 59350         | @SawyerMerritt Will visit IRS next time I’m in...
2022-02-20 09:43:28+00:00  | 1967          | @ID_AA_Carmack True
2022-02-20 08:51:40+00:00  | 11972         | @Erdayastronaut @Twitter @jack @TwitterComms S.

### Most used words in the user's Tweets
![image](https://user-images.githubusercontent.com/70821494/155210650-db82bd6f-5816-489b-af86-d00c5c6c41d1.png)

### Users and their tweets about Elon Musk

Users      | Tweet                                            | Created at                | Likes 
---------- | ------------------------------------------------ | ------------------------- | -----
jao_bala1  | elon musk                                        | 2022-02-21 04:59:18+00:00 | 0
SpilDil    | IM SELLING BITCOIN LIVE! COMPLETELY REAL WITH ...| 2022-02-21 04:58:35+00:00 | 0
cda621     | @flurnft Elon Musk, Nikola Tesla and other leg...| 2022-02-21 04:58:00+00:00 | 0
phat_yap   | @Uglyrat441 @TripSquadGoblin @DmanGrog @JDfrom...| 2022-02-21 04:57:54+00:00 | 1

