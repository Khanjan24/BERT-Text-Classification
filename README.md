# BERT-Text-Classification
Evaluation of different Natural Language Processing Models [Python]

## Executive Summary
Social media messaging is a significant resource to collect and understand human behavior. As this data is generated in abundant volumes on a minute basis, evaluating an automated technique to identify these behaviors would be very beneficial.  The goal of this project is to evaluate the performance of Google’s Bidirectional Encoder Representation of Transformers (BERT) in the classification of Social Media Texts. BERT was compared to four different classifiers: K-Nearest Neighbors (KNN), Support Vector Machine (SVM), Naïve Bayes, and Decision Tree (DT); and two neural network models – Recurrent Neural Networks (RNN) and Convolutional Neural Networks(CNN). Twitter posts associated with three commonly abused medications (Adderall, oxycodone, and quetiapine) were collected to classify users into those who are likely to abuse drugs and those who would not. BERT performed the best. Hyper-parameter tuning of BERT was performed to achieve the best results. 

## Requirements
1) To collect tweets from Twitter: Set up Twitter API access
A. Setting Up Your Twitter API Access:
- Create a Twitter developer account if you do not already have one, by visiting: https://developer.twitter.com/. (Note: if you do not have a Twitter account, you will need to create one first)
- Go to https://developer.twitter.com/en/apps and log in with your Twitter user account.
- Click “Create an app”.
- Fill out the form, and click “Create”.

Note: Where it asks for a website, you can provide a website if you have one, or a 'placeholder' (per the subtext). For instance, you can use your linkedin, facebook, etc. The url should be of the form: https:// (not http://).

- A pop up window will appear for reviewing Developer Terms. Click the “Create” button again.
- On the next page, click on “Keys and Access Tokens” tab.
-Copy your “API key” and “API secret” from the Consumer API keys section and paste them into your keys.py file where designated.
- Scroll down to Access token & access token secret section and click “Create”.
- Copy your “Access token” and “Access token secret” and paste them into your keys.py file where designated.
- Save your keys.py file. You're ready to start collecting tweets!

If at any point you get lost, here is a good tutorial that includes screen shots, which can help you to get set up (follow instructions until you reach R code). If using the tutorial, be sure to record your credential information in the keys.py file, as described above

2. Install the python-twitter library + Import the twitter and json libraries
!pip install python-twitter
import twitter
import json

## Objective
The aim of this project is to correctly identify users that are likely to abuse drugs from the Twitter tweets. 
Below is the basic framework of what was done.  

## Data Overview 
Initally when excuted a total sample of 3017 tweets were collected, with 447 (15%) categorized as “abuse” and 2570 (85%) categorized as “not abuse”. The data was split into training and testing set in the 80:20 ratio respectively. 
Prior to dividing the dataset into training and testing, the text was pre-processed. Since the tweets were written in the informal language in most cases, and contained reserved words related to Twitter, several steps were applied to clean the tweets.
- Twitter Specific Cleaning
- Stop word removal
- Case Conversion
- Lemmatization 
- Term replacement (eg. Replace (“Before,” “After”) -->  Replace (“quetiapine,” “seroquel”) since they are the same medication differed by generic and brand name. 

## Methodology
### Feature Selction & Resampling 
- Applied Term Frequency-Inverse Document Frequency (tf-idf), then created 3 datasets with a minimum of 20,30 and 50 term apperances 
- Experimented with 3 resampling techniques: Naive Random Overssampling, KNN based Synthentic Minority Oversampling Technique(SMOTE) and Naive Random Undersampling . 
- Applied all three resampling methods to the dataset with a minimum of 20-, 30- and 50-word frequency each and then performed the below 4 classification models to each scenario to compare model performance and determine the resampling method and the appropriate minimum frequency. SMOTE was the chosen method of resampling. 

###  Classification Models
- On the training set, four supervised classification models were performed to determine the best classification technique: KNN, Naïve Bayes, SVM, and Decision Tree.
- We focused on a multitude of performance metrics to determine the best classification model, mainly the F1-measure, recall value, and the model accuracy of the testing set.

### Neural Networks
- First performed tokenization, followed by padding and finally used class_weight since the dataset is unbalanced. 
- Performed RNN and CNN 
-Optimization

### Bidirectional Encoder Represntation of Tranformers (BERT)
- Pre-trained model: In this study, we used two models-- cased model and uncased model--to pre-train our data, which makes our data well fitted into BERT model.
- Hyper parameter tuning: We performed a total of 144 combinations of parameters from Batch sizes of [8, 16, 32, 64, 128, 256], Epoch sizes of [3, 4, 5], Learning Rates of [2e-5, 3e-5, 4e-5, 5e-5] and text Case of [‘Uncased’, ‘Cased’]. 
