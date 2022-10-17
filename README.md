# Portofolio
Welcome to my data analyst twitter
import tweepy
from textblob import TextBlob
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import re
import nltk
nltk.download('stopwords')
from nltk.corpus import stopwords
from nltk.stem.porter import PorterStemmer
from wordcloud import WordCloud
import json
from collections import Counter

#Part-1: Authorization and Search tweets
#Getting authorization
consumer_key = 'p6Fg6WjZeOIQN1FvrsnvCfcbo'
consumer_key_secret = '7sgTYd66QCOoaEDuOXSoH5TkoTJrzmWvjEDnVdIaO7tqZgeGhg'
access_token = '132425188-3pEgCTglpzvYC605OMINgGkn3fO5pTFMv2NfWY61'
access_token_secret = 'Qkzccwwbf6J4Mrpkem4LHVefHxBT13E3C28x0F8gufIyc'
auth = tweepy.OAuthHandler(consumer_key, consumer_key_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth, wait_on_rate_limit=True)

#Defining Search keyword and number of tweets and searching tweets
query = 'arab'
max_tweets = 2000
searched_tweets = [status for status in tweepy.Cursor(api.search, q=query).items(max_tweets)]

#Part-2: Sentiment Analysis Report

#Finding sentiment analysis (+ve, -ve and neutral)
pos = 0
neg = 0
neu = 0
for tweet in searched_tweets:
    analysis = TextBlob(tweet.text)
    if analysis.sentiment[0]>0:
       pos = pos +1
    elif analysis.sentiment[0]<0:
       neg = neg + 1
    else:
       neu = neu + 1
print("Total Positive = ", pos)
print("Total Negative = ", neg)
print("Total Neutral = ", neu)

#Plotting sentiments
labels = 'Positive', 'Negative', 'Neutral'
sizes = [257, 223, 520]
colors = ['gold', 'yellowgreen', 'lightcoral']
explode = (0.1, 0, 0)  # explode 1st slice
plt.pie(sizes, explode=explode, labels=labels, colors=colors, autopct='%1.1f%%', shadow=True, startangle=140)
plt.axis('equal')
plt.show()
