# Review Digest

##About
Online shopping is becoming more and more popular in recent times. And with increased importance and popularity of e-commerce websites, reviews have become a very important part of the complete online experience by shaping our opinion before we buy a product. However, the amount of effort required to form an opinion about different aspects / features associated with any product is huge, and repeating the same effort when trying to compare consumer opinions of different products adds to the complexity, and tediousness of the task.

In this project we aim to simplify and automate the task of identifying the various aspects being talked about a particular product in a review, extract these aspects and identify the sentiment associated with each of these aspects. In the end of this process, the user will have a summary of all the reviews listing the pros and cons of the specified product. We will be limiting the scope of our project to deal with cellphones only. We will be using Amazon reviews as the source of our analysis data.

##Technologies Used
- Web scrapping - Beautiful Soup
- Programming Language - Python 3.4
- Data Mining and Natural Language Processing library - NLTK
- Machine Learning and Data Analysis Library - Scikit Learn and Pandas
- Data Visualization - MatPlot 

## Analysis Steps
The entire task can be broken down into 3 broad steps:

- Product Attribute Extraction
- Extracting Review Phrases associated with each Product Attribute
- Opinion Sentiment Prediction

**Note:** For in-depth details, refer to the technical report **Review Digest Report.pdf**

###Product Attribute Extraction
We started with tokenizing the reviews into different sentences and tagging individual words in it. A manual inspection of different review sentences showed that most of the product attributes were either nouns, adjectives, adverbs or a combination of them. We then extracted only those word phrases which used certain Regex pattern for noun/adjectives/adverbs phrases and occurred a certain number of time.

Many of these extracted phrases were synonyms of each other. In order to club them into similar groups, we used the following 3 properties [*Clustering Product Features for Opinion Mining by Zhongwu Zhai, Bing Liu, Hua Xu, and Peifa Jia*] :

1. **Common Words**:
Attribute expressions sharing some common words are likely to belong to the same
group. For example, "battery life", "battery", "battery charger" etc.
2. **Lexical Similarity**:
Attribute expressions whose words are synonymous in WordNet are likely to belong in the same to the same group. For example, "battery" and "charger"
3. **Domain Filtering**:
Attribute expressions whose words are related with the application domain or product are likely to be most relevant product attributes. For example, "screen", "internet", "camera" are essential features of a cellphone and hence relevant.

###Extracting Review Phrases associated with each Product Attribute
Each sentence in the review were mostly complex, with multiple product attributes and multiple set of descriptors. In order to overcome these challenges, and correctly extract single attribute per phrase, we split the review sentences on conjunction and punctuations.

In order to associate each phrase with the corresponding product attribute it contained, we first created a dataframe for every extracted product attribute. We then used a simple algorithm to traverse through each phrase and find whether it contains a product attribute or its synonyms. If yes, then the phrase was added to corresponding attribute's dataframe. If a phrase contained multiple product attributes then the phrase was added to the dataframes of all the contained attributes.

###Opinion Sentiment Prediction
We used vectorizers to extract and learn syntactic patterns accompanying different sentiments in the reviews. We then trinaed classifiers on manually labelled training dataset to predict the sentiment contained in each of the phrases.

Thus, this step was separated into three segments:

1. Manually labelling the training set into positive, negative and neutral sentiments
2. Identifying the best vectorizer to extract characteristic features differentiating one sentiment from another
3. Identifying the best classifier which will used these characteristic features to predict sentiments

This involved finding which combination of vectorizer and classifiers works the best for the dataset, without over-fitting to the training dataset.

##Results
On the training dataset, the combination of Count Vectorizer and Logistic Regression Classifier gave a precision of 81%. However, running this combination on the test dataset made us realize that Count Vectorizer and Logistic Regression Classifier were over-fitting on the training data set and not producing as good results as expected.
On the other hand, though the combination of Tf-Idf Vectorizer and Random Forest Classifier was giving only 76% precision on the training data set, it was giving much better results on the test dataset.

##Contributors
- Ankur Kumar
- Keshav Potluri
- Richa Prajapati

