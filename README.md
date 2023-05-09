# Twitter-Keyphrase-Extraction

This project deals with extracting keyphrases from Twitter data for various NLP tasks such as sentiment analysis. 

A keyphrase is defined as a phrase that is highly relevant to the test or dataset. In this case, this means that the phrases that are most used across all tweets end up saying the most about the dataset. This model extracts the top 10 keyphrases ranked by scores assigned based on the similarity of their sentence embeddings with the dataset as a whole.

This is done using an ensemble of 3 sentence transformers:
- DistilBERT
- XLM-Roberta
- MiniLM

The process consists of 4 steps - 

<b><i> Step 1 - Preprocessing </i></b>

Datasets were obtained premade from Kaggle, but they can just as easily be scraped using either the Twitter API and Tweepy or the snscrape library
For preprocessing, mentions of other users, URLs, punctuations and the hash character were removed. Stopwords were also removed using the <i>stopwords</i> dictionary from nltk.
They were then put into a dataframe, so that they can be quickly accessed in further steps.

<b><i> Step 2 - Embedding Extraction </i></b>

Sentence embeddings for all tweets were extracted using each of the above three transformers. After that, the tweets were split into N-gram phrases and the embeddings of those phrases were then obtained using the same transformers.

<b><i> Step 3 - Similarity Calculation </i></b>

Similarity of each phrase with the whole dataset was calculated using cosine similarity between the phrase and every tweet in the dataset, and then the score of the phrase was calculated taking the average of all those similarities.

Since there were three sentence transformers used, each keyphrase will have three similarity scores associated with it

<b><i> Step 4 - Scoring and Ranking </i></b>

Before ranking, a threshold score 0.3 was set. If any tweet got a score below 0.3 using any of the sentence transformers, it would be removed from the dataframe. Once this was done, the similarity of each phrase with the dataset was calculated using the average of all three similarity scores calculated in the previous step.

Then the top 10 keyphrases were selected based on this ranking.


Reference Paper - [Link](https://ieeexplore.ieee.org/document/9641788)
