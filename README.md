# Toxic-Comments-Capstone
NLP Project on toxic commentary identification

Dataset Overview
The threat of abuse and harassment online prevent many people from expressing themselves and make them give up on seeking different opinions. In the meantime, platforms struggle to effectively facilitate conversations, leading many communities to limit or completely shut down user comments. Kaggle started a competition with the Conversation AI team, a research initiative founded by Jigsaw and Google. The competition could be found here: https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge

I am interested in Natural Language Processing. A project defining and identifying sentiment of language can be direct beneficial in making online discussion more productive and less negatively impactful. 

My aim was to build a model that is capable of detecting different types of toxicity like threats, obscenity, insults, and identity-based hate.

The dataset I used consists of comments from Wikipedia’s talk page edits. These comments have been labeled by human raters for toxic behavior. The toxicity labels are:

toxic
severe_toxic
obscene
threat
insult
identity_hate

There are 159,571 observations in the training dataset and 153,164 observations in the testing dataset. Since the data was originally used for a Kaggle competition, in the test_labels dataset there are observations with labels of value -1 indicating it was not used for scoring.

Data Preprocessing and EDA
All of the data is text comments. I wrote a tokenize() function, removing punctuations and special characters, stemming and/or lemmatizing the comments, and filtering out comments with length below 3. After benchmarking between different vectorizers (TFIDFVectorizer and CountVectorizer), I chose TFIDFVectorizer, which demonstrated better performance.

The major concern of the data is that most of the comments are clean (i.e., non-toxic), and continued imabalance between the positively identified toxic labels themselves. This indicates that I needed to deal with imbalanced classes later on. I used different methods, such as resampling, choosing appropriate evaluation metrics, and choosing robust models to address this problem.

Model Fitting
Evaluation Metrics Selection
During the modeling process, I chose multiple different evaluation metrics to evaluate the performance of models based on the nature of the data:
Recall
F Score
Hamming Loss
Basic Model Comparison
Using Multinomial Naive Bayes as our baseline model, I first used k-fold cross validation and compared the performance of the followingi three models without any hyperparameter tuning: Multinomial Naive Bayes, Logistic Regression, and Linear SVC. Logistic Regression and Linear SVC perform better than Multinomial Naive Bayes.

After checking how these models perform on the test data, Muninomial Naive Bayes did not perform as well as the other two models while Linear SVC in general out performs the others based on F1 score.

Overall, without any hyperparameter tuning, LinearSVC performs the best initially.

Pipeline with Manual Hyperparameter Tuning
After accounting for the imbalanced data, the F1 score of Logistic Regression model has jumped to an average of 0.9479 while Linear SVC has jumped to 0.9515.

Grid Search
With the help of grid search, I found the "optimal" hyperparameters for the models and was able to reach an average of the best score of 0.9566 for Logistic Regression and 0.9585 for Linear SVC.

Ensembling
To ensemble different models, I tried a few models based on tree boosting, then used a voting classfier to ensemble one of the boosting model with the basic models in previous parts, resulting in an F1 score of 0.973566 and Hamming Loss of 0.024639 using Ensembling.

Results

In terms of evaluation metric, Linear SVC performs the best. 

I believe after tuning hyperparameters for ensembling, I will achieve better results. 

I chose Linear SVC as the optimal model. Linear SVC trains model the fastest. Refering to interpretability, Linear SVC is also easier for the users to understand and has a simpler internal processing. 

