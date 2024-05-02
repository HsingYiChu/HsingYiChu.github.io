## Hotel review and rating prediction - practice of unstructured text data analysis

**Project description:** This project mainly focused on practising text analysing tools, including Bag of Words (BOW) and Term Frequency-Inverse Document Frequency (TF-IDF), on a dataset that contains a review section (text) and ratings (numerical grades). Furthermore, after the analysing tools gave us the numerical representation of the texts, a regression model was applied to predict the rating.

### 1. Data preparation

Explore the word frequency in the dataset after removing stop words and some highly mentioned neutral words (e.g. hotel) from the text.
<img src="images/hotel_review_word_freq.png?raw=true"/>

Further remove unnecessary symbols

'''
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
'''
