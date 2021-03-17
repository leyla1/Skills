# Skills 
# Preprocessing of data 
# Import libraries 

import pandas as pd 
import numpy as np 
import re
import string
import spacy 
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer
import nltk
import numpy as np
import sys
from collections import Counter
import matplotlib.pyplot as plt 


# removing : Numbers, white spaces removal, punctuation,  
dictionary = {'ä':'a','ë':'e','ï':'i','ö':'o','ü':'u','ÿ':'y'}
pd.set_option ('display.max_colwidt',-1)
data = pd.read_csv('Skills.csv', error_bad_lines=False, encoding='latin1', delimiter=';')
data.replace(dictionary, regex=True, inplace=True)
data['Omschrijving'] = data['Omschrijving'].str.strip()
data['Omschrijving'] = data['Omschrijving'].str.lower()
data['Omschrijving'] = data['Omschrijving'].str.replace('\d+', '')
data['Omschrijving'] = data['Omschrijving'].str.strip()


# Removing stopwords
data['Omschrijving'] = data['Omschrijving'].apply(lambda x:[item for item in str(x).split() if item not in stopwords.words('dutch')])
#print(data['Omschrijving'])


# Split the word in tokenize 
#def custom_tokenize(text):
#    if not text:
#        print('The text to be tokenized is a None type. Defaulting to blank string.')
#        text = ''
#    return word_tokenize(text)
#data['tokenized_column'] = data['Skill omschrijving'].apply(custom_tokenize)

# Object to string 
data.Omschrijving = data.Omschrijving.astype('string') 
#print(data.dtypes)

# count words 
result = Counter()
#data['Omschrijving'].str.lower().str.split().apply(result.update)
data_list = []
data_list = data['Omschrijving']
print(data_list.str.lower().str.split().apply(result.update))
#print(result)

# Make a histogram of words 
counts = Counter(data['Omschrijving'])
labels, values = zip(*counts.items())
indSort = np.argsort(values)[::-1]
labels = np.array(labels)[indSort]
values = np.array(values)[indSort]
indexes = np.arange(len(labels))

# set the histogram 
bar_width = 0.35
plt.xlabel('word', fontsize=12)
plt.ylabel('count',fontsize=12)
plt.bar(indexes, values)
plt.xticks(indexes + bar_width, labels)
plt.show()

# Count frequency of words in pandas DataFrame 
# skil = data['Skill omschrijving'].str.cat(sep=' ')
# df = (data['Skill omschrijving1'].str.split(expand=True).stack().value_counts().rename_axis('vals').reset_index(name='count'))
# print(data['Skill omschrijving'].value_counts


