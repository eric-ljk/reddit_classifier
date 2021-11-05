<img src="http://imgur.com/1ZcRyrc.png" style="float: left; margin: 20px; height: 55px">

# Project 3 - Web APIs & NLP

--- 

# Executive Summary

Anyone tracking the latest trends in technology would have a need for tools and metrics to determine a brand's Share of Voice in the market. This includes writers, YouTubers, tech enthusiasts and investors. With Apple and Samsung being the notable heavyweights in the smartphone domain, the battle has become increasingly heated with more eyes on the two. To this end, the Editor-in-chief of a tech magazine has asked for a classifer tool to scan online tech forums to see if more people are talking about Apple or Samsung.

A project was undertaken to build this tool using machine learning. The Pushshift API was used to pull posts from the subreddits r/Apple and r/Samsung. The API is a data-fetching tool created by the moderators of r/datasets. After some data processing, 4000 of the most recent posts from each subreddit were used for modelling, totalling 8000. The text of the title and post body were combined and taken as the text for each post. Before modelling, Natural Language Processing indicated that many people tended to ask product-troubleshooting questions on the subreddits.

For modelling, the Multinomial Naive-Bayes model, Logistic Regression model, Support Vector Classifier model and Random Forest model were tested and optimised. The chosen model was Logistic Regression. The classifiers were primarily evaluated by their accuracy score, and a successful model should have an accuracy score of at least 0.8. The accuracy score represents how many posts the model predicted correctly, divided by the total number of predictions made.

Logistic Regression produced an accuracy score of 0.956 on the testing subset of the data, with 0.973 on the training subset. This was a tie with the Support Vector Classifier, but its score of 0.996 on the training subset showed that the Support Vector Classifier overfitted more to the training data. This made Logistic Regression a more favourable choice. Logistic Regression was also more interpretable than the Support Vector Classifier, being able to show which words were the strongest predictors for classification into a particular subreddit. In this case, it was found that the brand and product names were the strongest predictors.

To sum up, the project endpoint was achieved, and the tool is ready to be deployed and further tested by the tech magazine.

# Problem Statement

You are a data science professional working for a tech magazine discussing the latest trends in technology. The Editor-in-chief wants to come up with a big year-end story that reveals the most-talked about tech brand of the year. She is intending to scan online tech forums to see if more people are talking about Apple or Samsung. However, she cannot possibly scroll through the forums manually.

As the first step to tackling this, you have been directed to build a text classifier that can detect if any given online post is talking about Apple or Samsung. This classifier will be primarily evaluated by its accuracy score, and a successful model should have an accuracy score of at least 0.8.

# Background and Research

Share of Voice is the measure of how much of the market represents your brand, and can be measured by metrics like keywords ([*source*](https://sproutsocial.com/glossary/share-of-voice)). The tech market has been dominated by a few major players, and Apple and Samsung are the notable heavyweights in the smartphone domain. 

Although the iPhone has the dominant share of voice in general, when the share of voice was split into the topics of cost, design and features, it was found in an analysis that Samsung was leading in share of voice regarding cost and design. The iPhone led in share of voice regarding features ([*source*](https://hottopics.ht/9526/iphone-losing-smartphones-share-of-voice-war/)). From the same analysis, it was discussed that the ubiquitiy of Apple may have led to people talking about other brands instead. 

It is thus important for any analyst of tech trends to keep abreast of the current changes in the market. Apple and Samsung are direct competitors in the mobile phone space, releasing competing flagship models within the same frame of time ([*source*](https://www.which.co.uk/reviews/mobile-phones/article/apple-iphone-vs-samsung-galaxy-mobile-phones-aZL5V5m4UGbw)). Apple's market share based on sales figures was 20.8% in in Q4 2020, while Samsung's market share was 16.2% ([*source*](https://www.zdnet.com/article/apple-vs-samsung-who-makes-a-better-smartphone/)). There is thus a close fight between the two, and tech users will be eager to know what is the latest state of affairs between the two companies. 

Apple had $111 billion in sales for the Christmas of 2020 ([*source*](https://www.bbc.com/news/business-55835504)). Meanwhile, Samsung is trying to keep up by improving the features on its phones, such has having a fingerprint sensor embedded in the screen ([*source*](https://www.businessinsider.com/samsung-galaxy-s20-ultra-apple-iphone-11-features-specs-camera-2020-2#higher-resolution-camera-sensors-3)) and fast charging ([*source*](https://www.samsung.com/us/support/answer/ANS00062589/)). 

The Pushshift API it can be used to obtain the data from the subreddits. It is a tool made by the moderator team of r/datasets ([*source*](https://github.com/pushshift/api)). The text that forms the body of the posts will play a large role in the analysis. Sentences are about 15-20 words long, so there is a guideline in mind when determining if the length of a segment of text contains at least a sentence ([*source*](https://techcomm.nz/Story?Action=View&Story_id=106)).

# Data sources

The data was retrieved from the subreddits r/Apple and r/Samsung using the Pushshift API.

# Data Dictionary

The Data Dictionary is as follows:

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**text**|object|ap_ss|Combined text of the title and post body.|
|**subreddit**|object|ap_ss|Subreddit that the post belongs to.|

# Results and Analysis

The models with their details and metrics are as follows:

|Model|Test Accuracy|Training Accuracy|F1 Score (Apple)|F1 Score (Samsung)|ROC AUC|Vectorization|
|---|---|---|---|---|---|---|
|**Dummy Classifier**|0.496|0.501|0.000|0.664|0.500|Count|
|**Multinomial Naive-Bayes**|0.946|0.949|0.945|0.946|0.984|Count|
|**Logistic Regression**|0.956|0.973|0.956|0.956|0.991|TFIDF|
|**Support Vector Classifier**|0.956|0.996|0.956|0.956|0.991|TFIDF|
|**Random Forest**|0.953|1.000|0.952|0.953|0.990|TFIDF|

Logistic Regression is tied with Support Vector Classifier across all the metrics. However, Logistic Regression takes much less time to run and is more interpretable (feature importances can be obtained). Just to note, if we go one more decimal place down the ROC AUC score, Logistic Regression is higher at 0.9907 versus 0.9905 for the Support Vector Classifier. Finally, the difference between the training accuracy and the test accuracy is higher for the Support Vector Classifier as opposed to Logistic Regression. This means that the Support Vector Classifier is overfitting more than Logistic Regression. 

Therefore, the model of choice is Logistic Regression.

# Conclusion and Recommendations

In summary, we have achieved a successful model as defined by our problem statement. The test accuracy score was 0.956, which is higher than the stipulated 0.8. The model chosen was Logistic Regression. The training accuracy score was 0.973, which meant that the model did not overfit severely to the training data. The 5-fold cross-validated training score of 0.94 was close to the test score as well, which meant that the test score was a reliable measure.

This was a tie with the Support Vector Classifier, but its score of 0.996 on the training subset showed that the Support Vector Classifier overfitted more to the training data. This made Logistic Regression a more favourable choice. Logistic Regression was also more interpretable than the Support Vector Classifier, being able to show which words were the strongest predictors for classification into a particular subreddit. In this case, it was found that the brand and product names were the strongest predictors. Logistic Regression was much faster in modelling as compared to the Support Vector Classifier as well.

Natural Language Processing indicated that many people tended to ask product-troubleshooting questions on the subreddits. Hence, modelling does not have to be the only way to generate insights to help achieve the objective of writing a magazine article about the most-talked about tech brand of the year. Further analyses could be done in the form of sentiment analysis, where the proportions of positive and negative words and their context could shed light on brand sentiment. This would reveal more than just whether people are talking about the brand. Also, the model could be tested on other types of social media postings such as Facebook posts, to see how well it is able to generalise.

To sum up, the project endpoint was achieved, and the tool is ready to be deployed and further tested by the tech magazine.