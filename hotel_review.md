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

Split the data into train-test split where 50% of data will be used as test set, set review as X and rating as Y, we will then have 4 groups of data -- X_train, X_test, y_train, y_test. For the Y groups, additional binary labels were created by assigning ‘1’ – positive for the product ratings 4 and 5; and "–1" for product ratings 1, 2 and 3. Store it in y_train_binary and y_test_binary. Furthermore, for the reviews (X), BOW and TfIdf were apllied respectively to create two numerical representation.
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

### 2. Model Training

Define 3 Logistic Regression models: model1, model2 and model3 and train the models as follows:
1. Train the first Logistic Regression model using the Bag of Words representation (train_data_BOW) to predict the hotel rating (Y).
2. Train the second Logistic Regression model using the TfIdf representation (train_data_tfidf) to predict the hotel rating (Y).
3. Train the third Logistic Regression model using the TfIdf representation (train_data_tfidf) to predict the binary sentiment label (Y_binary).
Make and store predictions on appropriate test sets (X_test_BOW for model1 and X_test_tfidf for model2 and model3)
```
# code for model1 

from sklearn.linear_model import LogisticRegression
# define lgositic regression model object
model1 = LogisticRegression(random_state=random_state)

# fit the model to training data
model1.fit(X_train_BOW, y_train)

# create BOW for test data
X_test_BOW = vectorizer.transform(X_test)

# predict using model 1 object
y_test_model1_predictions = model1.predict(X_test_BOW)
```

### 3. Model Evaluation

Compute and compare the test accuracy of Model 1 (Logistic Regression with BoW representation) and Model 2 (Logistic Regression with TfIdf representation). Based on your results, determine which embedding method yields higher performance in predicting the hotel ratings (Y).



