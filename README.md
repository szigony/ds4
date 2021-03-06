# Text and Sentiment Analysis of The Most Popular songs of the last 50 years

This was a term project for the _Data Science 4: Unstructured Text Analysis_ course at the Business Analytics masters at the Central European University of Budapest. The project's aim is to identify topics, keywords and sentiments that result in the most popular songs.

__Table of contents:__

* [Goal of the analysis](#goal-of-the-analysis)
* [About the Data](#about-the-data)
* [Packages used](#packages-used)
* [Term Frequency Analysis](#term-frequency-analysis)
  * [Most frequently used terms](#most-frequently-used-terms)
  * [Trends](#trends)
  * [TF-IDF](#tf-idf)
* [Sentiment analysis](#sentiment-analysis)
* [Topic Modeling](#topic-modeling)
* [Summary](#summary)
* [Afterword](#afterword)

## Goal of the analysis 

The goal of my analysis was to determine what makes a song popular from a linguistic point of view.

When I originally came up with the idea that I want to analyse lyrics, I thought it would be interesting to see difference in genres, but than I thought about how my music consumption changed over time. My favorite songs talk about very different topics nowadays than 5-10 years ago. Is it just me, who while growing up started to listen to all kinds of different music, with deeper meaning, or it's a general trend we can see over time? Do the most popular songs always talk about the same things, or do they have different topics? Do these topics change over time? Could we maybe use text analysis to come up with a song ourselves?

These are the questions that I would like to answer using the methods I acquired in class.

## About the Data

The dataset I use to answer these questions is all the lyrics from the songs that lead for at least a week the Billboard Hot 100 music toplist from 1970 to 2018. 

This information is sourced from two different websites. One of them is the [Billboard](https://www.billboard.com/charts/hot-100) website itself, from where I get the archives of the Hot 100 chart going back until 1970. The other one is [Genius](https://genius.com/), source of music related news and lyrics. 

Due to the nature of these songs - one can have multiple artists, the name of the songs or artists can be challenging to interpret -, I was unable to automatically pull the lyrics for each and every song, however most of the data I needed to work with was relatively easy to get. 

Before pulling the lyrics for the songs however, I made sure to select the distinct Artist - Song combinations. This means that I'm not accounting for how long a certain song lead the toplist, only for the fact that it was there. This choice was a concious decision based on the fact that once a song gets to the top, I consider it successful enough that differentiating between a song that hold the top position for 1 and another that held it for 3 weeks doesn't help us tremendously in my goal of answering my research questions.

## Packages used

What made this analysis possible was the mostly used text analysis packages, such as the `stringr`, `tidyr`, `tidytext`, `wordcloud` and `dplyr` packages, and some other ones that are used by most of the data science projects nowadays, such as `ggplot2`, `data.table`, `tibble` and such. 

Also, the [genius](https://github.com/josiahparry/genius) package created by JosiahParry was very useful in extracting lyrics for the songs. The package had some limitations, but I was able to work with it successfully.

## Term Frequency Analysis

In my analysis I focus on the most popular words used in the most popular songs, and try to come to a conclusion on some trends and topics that are either very distinguisable from each other or are used in almost all the examined songs. 

### Most frequently used terms

The first step of this process is looking at the words which were used the most.

![alt text](https://github.com/molnardan95/ds4/blob/master/Charts/most_frequent_words.png)

As we can see on the chart above, the most frequent words are all - somewhat - related to one topic, which is relationships, more specifically "love". If we were to extend the selection, we would also get words like "dance", "heart" and some others, but the general topic doesn't change much. It's mostly boys and girls and their feelings for each other. 

### Trends

Let's see if this changes if we include a time dimension. 

![alt text](https://github.com/molnardan95/ds4/blob/master/Charts/most_frequent_words_by_decade.png)

The answer is not really! We see some slight differences, however these are very minor. There are some new words surfacing, such as "hey" or "hot", but these are still related to the same topic in the examined songs. 

A very interesting case is the word "ron" in the 1970s. There are two songs which contain this word a lot of times, "Da Doo Ron Ron" by Shaun Cassidy and "Bad Blood" by Neil Sedaka. In neither of these songs does this word have any meaning, it's more of a playful word that is mentioned so many times that it made it to the toplist in that decade.

One thing we can say for sure is that the most frequently used words did not change much over the years, and that they cover one or two very simple, easy to understand topic that everyone can relate to. 

![alt text](https://github.com/molnardan95/ds4/blob/master/Charts/most_frequent_words_wordcloud.png)

### TF-IDF

There must be something that makes these decades unique right? It can not be that over this very long period of time throughout which multiple generations grew up, all the songs are the same. Or is it possible?

By looking at the TF_IDF values for each words by decade, we can identify those that make each decade different from each other.

![alt text](https://github.com/molnardan95/ds4/blob/master/Charts/tf_idf_words_in_decades.png)

Again, it seems like that we can't generalize a distinct topic for any of the decades. We can infere a couple of interesting things however. In the 70s and 80s, mentioning peoples names were more frequent, that's why we see names like "diana", "sara", "louie" and such in these decades. In the later decades after 2000, more swear words are used, such as "shit" or "fuckin". Also, we identify some well known songs from these centuries, such as "Uptown Funk" by Bruno Mars in the 2010s, "Womanizer" by Britney Spears in the 2000s and "Macarena" in the 90s. 

Other than these, the tf-idf analysis seems to confirm that popular music didn't change much over time. 

## Sentiment Analysis

So did the sentiment change at least? Do we see any general trends of decades where the sentiment was better? Can we see a general decline or improvement?

![alt text](https://github.com/molnardan95/ds4/blob/master/Charts/decade_sentiment.png)

Using the BING lexicon for sentiment analysis, we do see some kind of a decline in general. To make sure that this is true, I used the 3 most frequently used sentiment lexicons, to see if this trend could be something that's actually real, or is there some bias in the lexicon itself.

![alt text](https://github.com/molnardan95/ds4/blob/master/Charts/sentiment_all_3_packages.png)

It seems like there is such a trend. Sentiment seems to be going down over time. Does that mean that people listen to more negtaive music in the new millenia? Well, sort of. While I was trying to identify what is causeing this shift in sentiment I came to two conclusions.

![alt text](https://github.com/molnardan95/ds4/blob/master/Charts/sentiment_contributor_words2.png)

First, there does seem to be a downward trend, but it might not be so significant as it is on the previous chart. The reason for that - which was my second observation - is that songs use language like "wild", "shake", "crazy" and "shit" more often lately and these words are not always used in a negative context. 

Lastly we can also check how the distribution of the words with the most effect on sentiment changed over time on the below chart.

![alt text](https://github.com/molnardan95/ds4/blob/master/Charts/usage_trend_most_sentimental_words.png)

It is quiet consistent with less "love" and more "bad" lately. 

## Topic modeling

So is there anything that makes anything unique at all? Are these songs all just the same at the end of the day. There is a very slight shift in words used and sentiment, but based on all of the above, I started to highly doubt that people listen to different music now then 50 years ago. Topic modeling is our last hope.

The easiest choice for me was to make the LDA function create 2 distinct topics out of all the words used. If the 2 topics are very similar, creating more topics won't enhance my analysis any further.

![alt text](https://github.com/molnardan95/ds4/blob/master/Charts/decade_topic_modeling.png)

To the surprise of no one at this point, the two topics that were created are essentially the same. There are some slight differences, but most of the frequent words are the same. It's nothing but love throughout the centuries. 

One interesting thing is that the function did group together the two latest decades into one of the topics and the earliest three decades into the other one. We can see the most unique words in these two distinct topics, and we can identify similar things to what we have previously. There are some songs standing out, that make these decades different from each other, but they are still very very similar to each other.

![alt text](https://github.com/molnardan95/ds4/blob/master/Charts/topic_unique_words.png)


## Summary

I started out with the intention to see what are the topics, words and sentiments which make a song pouplar. To answer these questions, I used the songs that lead the Hot 100 Billboard list over the last ~50 years. It turns out, that most popular songs are very similar to each other. All they talk about is love, girls, and relationships in general with very simple words used most of the time. Even though there is some noticable change in sentiment that could be mostly due to the change in words when these artists sing about this topic.

So is this all you need? Just use some simple words about love, make them rhyme and success will follow? Well, probably it is not enough. You will also need a cathy tune, and an artist who can deliver such high quality, but picking words from the results of this analysis could definitely be a good start to make it big on the Hot 100 list, to be the most popular.


## Afterword

It is important to mention the bias in my analysis. There could be more thorough analysis done if I were to include not just the top 1 songs of each week from this list, but downloaded the top 10/50/100. I imagine that the result would be slightly different. Also, I only used the songs that were on the top of this one specific toplist. Other toplists might have different songs leading the charts, from maybe more diverse genres. 

In the end, it does makes sense that the most popular songs are about a topic - love - that almost everyone can relate to, as all of us have experienced a feeling similar to it. 
