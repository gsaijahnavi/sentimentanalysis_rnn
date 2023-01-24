# INTRODUCTION
In tech, Apple vs Samsung is one of the biggest battle. We are aiming to do a competitive analysis between iphone and samsung smartphones through sentiment analysis from tweets. The battle between Apple's OS and Android always prevails. There is a section of people who wants to use nothing except apple unlike the section of people who do not want to be in Apple's ecosystem. We are scraping tweets from @SamsungNewsUS and @iPhone_News to compare the sentiments associated with them. It is an interesting topic to compare and understand the sentiments across these products. With the increasing popularity of these products expanding each day, this competitive analysis will help understand the market share of each product.

Apple takes first place for smartphones: 43 percent of US consumers reported purchasing Apple branded smartphones in the last year vs 29 percent purchasing Samsung (Source: TraQline, 4QE June 2021. However the global market tells a different story. On the international stage, Samsung ships more smartphones than any other manufacturer, while Apple held second place last quarter. (Source:https://www.traqline.com/newsroom/blog/competitive-analysis-apple-vs-samsung-market-share/)

So this sentiment analysis will help us to understand the emotion weightage across these two brands and will help in assessing the market performance of both the brands. Understanding the performance of these two highly competitive brands will help in many ways. One of the major contribution would be to make decisions on portfolio investment.

# ANALYSIS
* We tried different twitter handles to finally come into this conclusion, we observed there is some inconsistency in the tweets that were scraped. For some of the handles there were not enough tweets. For others there were tweets in other languages written in english.

* Language inconsistencies created problem when we performed modeling (especially model 2) where we used glove word embeddings (that are extracted from english wikipedia)

* Initially we started running with 1000 tweets for Samsung, Iphone each, but we saw an improvement in results when we increase the number of tweets to 2000 for each.

* Initially in model 1, we used ecodings of tf-idf for the entire dataset and proceeded with train, test split, however we realised that this is causing data leakage leading to incorrect results.

* We changed the approach by performing lemmatization first and then perform train test split. We used TfidfVectorizer() to fit transform on train set and then transform on validation and test set. By doing these changed R2 is improved by ~25% (0.09 to 0.32)

* In model 2, Intial models are constructed with only two layers which did not yield good results so, we changed the architecture by adding two more layers and increasing the numnber of nodes then the model r-squared increased.

* Glove embeddings are used in the model. These are set to be un-trainable. We could try training these embeddings from glove to obtain better results.* Overall, model-2 was not able to steal the logic of NLTK package.

* In model3, We tried several models by building components over simple RNN like 1D CNN, Bidirectional LSTM. With increase in complexity we observed the model is not able to generalize well on training data due to insufficient data. We tried and observed improvement in results by increasing dataset size to 3K, 4K. However due to exponential increase in run time we have stopped at 2K.

* In model3, for negative sentiment we see a distorted Actual vs Predicted plot. When we observed the distribution of negative we can see 95% of samples are concentrated at 0. Hence our monster model is finding difficulty in predicting higher values of negative sentiments.

* SentimentIntensityAnalyzer is a predefined model limiting the scope to fine tune it. Deep learning on the other hand has different models to explore such as RNN, Dense, LSM, GRU etc. Model weights can be tuned by introducing these layers to the model.

* Out of three models, our model I is able to stole the concepts of SentimentIntensity analyzer
