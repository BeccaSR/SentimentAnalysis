# SentimentAnalysis

The Dataset
The dataset used was downloaded from Kaggle, and is a selection of user product reviews for various Amazon products including Fire HD 8 Tablet, Amazon Kindle Lighted Leather Cover, Kindle Voyage and Amazon Fire TV Stick.

The dataset consists of 34,660 rows, and 21 columns. The columns include:
id, name, brand, categories, keys, manufacturer, reviews.date, reviews.dateAdded,, reviews.didPurchase, reviews.doRecommend, reviews.rating, reviews.text and reviews.title.

The following columns contained little to no data:
reviews.didPurchase, reviews.id, reviews.userCity and reviews.userProvince


The Preprocessing Steps
In order to process the data ready for Sentiment Analysis, I took the following steps:
Selected the ‘reviews.text’ column, and saved this to the reviews_data variable. This is due the fact that the dataset contained a number of columns, but we were only interested in the content of the reviews.text column.
Remove all null values. Before data cleaning, there were 1 null values in the reviews data. dropna was therefore used to remove all rows with no data. 36,459 reviews remained,

The following steps took place in the preprocess function, which preprocesses one review at a time:
The review text passed through the function was converted to lowercase string, and passed through the spacy model (nlp). This was saved to the doc variable.
Using a for loop, each word in the text was then checked if it was a stop word or punctuation - if the word was a stop word or punctuation then this would be skipped and not included in the processed review.
For each non-stop word, the word was lemmatized to convert it to its base form and also converted to lowercase. These words were then saved in the ‘processed’ list.
Finally, the preprocess function returns a string containing the processed words from the review.

	Example of review before preprocessing:
‘The kindle is easiest to use, graphics and screen crisp, clear, brilliant colors.’

	Example of review after preprocessing:
	‘kindle easiest use graphic screen crisp clear brilliant color’


Evaluation of Results
The model analysed the sentiment of all reviews in the dataset, and returned a total of 30,779 positive reviews, 1,662 negative reviews and 2,218 neutral reviews.
This shows that there are an overwhelming majority of positive reviews in the dataset for the product.

The review in Section 2 above returned a positive sentiment.

Example reviews and their returned sentiment:
The review: This product so far has not disappointed. My children love to use it and I like the ability to monitor control what content they see with ease.
Sentiment: Positive
The review: this tablet is perfect for surfing the internet and following social media
Sentiment: Positive
The review: I hate the ads. They are annoying and you cannot get them off. It's super confusing how to even get to the home page
Sentiment: Negative
The review: We bought this to stream TV so we could cut our cable bill. Streaming live TV with Playstaion Vue and watching movies through Amazon Prime has worked well. We also have the less expensive Fire Stick and this product works much better.
Sentiment: Negative

Whilst the reviews a, b and c appear to match the sentiment given by the model, review d does not read as a negative review despite being scored as having a negative sentiment. This may be due to negative words such as ‘cut’, ‘bill’, ‘less’ and ‘expensive’ being included in the review; the overall sentiment is not being reviewed but rather the individual words.

This suggests that overall, the model can predict the sentiment of most reviews but its precision is limited.


Model Strengths and Limitations
One strength of the sentiment analysis model is its efficiency, facilitated by the preprocessing approach. This only occurs when each review is called rather than preprocessing all reviews beforehand. This design choice contributes to quicker execution times, making the model suitable for real-time sentiment analysis needs.

Generally, the model demonstrates consistency in aligning the predicted sentiment with the content of the review. Through using spaCy for tokenization and lemmatization, the model ensures the review data is normalised which ensures more accuracy of the sentiment analysis for similar words.

The use of spaCy and TextBlob for the model can be seen as a limitation of the model, as they may not be the most appropriate choice for specialised sentiment analysis tasks. In particular, spaCy lacks specific training for sentiment analysis, which may result in lower accuracy and performance than dedicated sentiment analysis models.

A further limitation of the model is the oversimplification of the sentiment interpretation, providing only positive, negative or neutral classifications. This output may not capture the full range of sentiment complexities in the reviews.
