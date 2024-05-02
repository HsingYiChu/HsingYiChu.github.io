## Hotel review and rating prediction - practice of unstructured text data analysis

**Project description:** This project mainly focused on practising text analysing tools, including Bag of Words (BOW) and Term Frequency-Inverse Document Frequency (TF-IDF), on a dataset that contains a review section (text) and ratings (numerical grades). Furthermore, after the analysing tools gave us the numerical representation of the texts, a regression model was applied to predict the rating.

### 1. Data preparation

Explore the word frequency in the dataset after removing stop words and some highly mentioned neutral words (e.g. hotel) from the text.
<img src="images/hotel_review_word_freq.png?raw=true"/>

Further remove unnecessary symbols
```
import re
def clean_data(text):
    # Format words and remove unwanted characters
    text = re.sub(r'https?:\/\/.*[\r\n]*', '', text, flags=re.MULTILINE)
    text = re.sub(r'\<a href', ' ', text)
    text = re.sub(r'&amp;', '', text) 
    text = re.sub(r'[_"\-;%()|+&=*%.,!?:#$@\[\]/]', ' ', text)
    text = re.sub(r'<br />', ' ', text)
    text = re.sub(r'br', ' ', text)
    text = re.sub(r'\'', ' ', text)
    return text
for n in range(len(df)-1):
    clean_data(review[n]) 
```

Split the data into train-test split where 50% of data will be used as test set, set review as X and rating as Y, we will then have 4 groups of data -- X_train, X_test, y_train, y_test. Furthermore, for the reviews (X), BOW and TfIdf were apllied respectively to create two numerical representation.
```
from sklearn.feature_extraction.text import CountVectorizer
vectorizer = CountVectorizer(stop_words = stop_words, min_df=0.01)

# fit the vectorizer object to train data
vectorizer.fit(X_train)
vectorizer.fit(X_test)

# get the BOW for train data
X_train_BOW = vectorizer.transform(X_train)
X_test_BOW = vectorizer.transform(X_test)

from sklearn.feature_extraction.text import TfidfVectorizer
vectorizer2 = TfidfVectorizer(stop_words = stop_words, min_df=0.01)

# fit the vectorizer object to train data
vectorizer2.fit(X_train)
vectorizer2.fit(X_test)

# get the TfIdf for train data
X_train_tfidf = vectorizer2.transform(X_train)
X_test_tfidf = vectorizer2.transform(X_test)
```


