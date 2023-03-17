# Topic-Modeling-and-Sentiment-Prediction
Introduction:-

• The goal of the assignment is to find out if using the Topic Modeling information helps improve the classification accuracy in this problem. We are using the training dataset of the Kaggle competition from https://www.kaggle.com/datasets/manchunhui/us-election-2020-tweets. We will be cleaning the tweets and using sentiment analysis to predict whether the tweet is positive or negative. We will also Implement LDA in spark to find topic composition and use logistic regression to find out whether the accuracy increases or not when the topic Modeling data is added.

Explanation:-

• Imported necessary spark libraries and spark session. Imported csv file with spark.read.csv.
• Selected only the tweet column which consists of the tweets data.
• With help of re regular expression and sql udf removed links, users, higher case, punctuations, digits, and extra spaces .
• Dropped null value rows.
• Created Polarity and Sentiment functions to find out the sentiment with the help of TextBlob. Added a sentiment column with values of 0(negative) or 1(positive).
• Further used sparknlp to split the data by words using documentAssembler, tokenizer, normalizer, lemmatizer, stopword, pos_tagger, ngrammer, finisher. Used a Pipeline to execute all the nlp functions.
• The pre-processed data is stored in final column and now I did CountVectorizer and IDF for creating a LDA model.
• Created a LDA for the IDF vector to find the important words for each topic. Initially number of topics taken was 5 and then tuned the number like 40 . After that used vocabulary to find the top 20 words on each topic and their indices.
• Now added sentiment to the data of lda model for the calculation of LogisticRegression model.
• With number of topics as 40, I did 10-fold cross-validation on the logistic regression model with rmse as evaluator and calculated the Roc for the model. Got rmse of 0.4931969619160719 and Area under ROC Curve is: 0.7659.
• Combined the topic distribution data and feature data using VectorAssembler to check the difference in evaluation accuracy.
• Repeated 10-fold cross-validation on the logistic regression model with topic distribution data and got rmse as 0.505008472252674 and Area under ROC Curve is: 0.8411
• At the end, implement pyLDAvis using sklearn and to get a creative interactive model of topics and words.
• For running the spark program. I used a py version of ipynb program with the help of AWS S3 , AWS EMR and putty to run the code on a cluster.
Conclusion:-
Pre-processing of the csv file is done successfully by Removing all columns except tweet, removed non-english tweets, user data , links, converting string to words , removing stopwords and converting the data into vectors .Used LDA to find the topic composition and the most important words in each topic with also their indices. With number of topics as 5 , I received a better prediction without the topic distribution included but when number of topics were 40 then I got better ROC with topic distribution. Also tried with other many numbers of topics . Thus, I find out how using the Topic Modeling information helps improve the classification accuracy in this problem and how to use pyLDAvis to visualize the tweets.

Instructions to run code:
1) install proper spark version and pip install all necessary libraries.
2) open the code stored in code/ FinalSourceCode.ipynb through a notebook(possibly Jupyter notebook).
3) run the program.
