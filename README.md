# Project3
# Using Song Lyrics to Predict Genre and Hit Songs and Identify Distinctive Topics and Keywords for Each Genre

**PART ONE:** Multi-class Classification trying to predict song genre from lyrics

**Obtaining Data:** Where did we get our data?

Two CSV's from Kaggle: one contained 300,000 song lyrics with genres, song names and artists. The other contained 12,000 songs and whether or not they have been on a top 100 song list during their time.

### Cleaning Data

This took a long time due to the fact that the lyrics and song titles were scarped fro mdifferent places so there was a lot of messy syntax, punctuation and foreign words we had to remove from the data - most of day one and some of day two.
We used a combination of  NLTK, Pandas and regex methods for cleaning the text, stemming, lemmatizing, removing stopwords, tokenizing, appending the clean lyrics back to the Pandas DataFrame.

**Exploring Data:** Looking at our Pandas Dataframe we found…

First thing we did was check for non-values and dropped songs with NaN and after cleaning we still had 200,000 rows.
Then we looked at value counts for Genre decided to drop Folk, Indie, and Other because the first two didn't have enough data and Other doesn't provide any predictive value.

After all of this cleanup we were left with eight basic genres: **Rock, Pop, Hip Hop, Metal, Country, Jazz, Electronic, R&B**. These are the target classes that we are trying to predict.
Distribution between genres was uneven, so we decided to randomly select 900 songs per genre giving us a total number of rows **900 songs * 8 genres = 7200 songs.**

### Feature Engineering and Model Optimization:

After stemming and lemmatizing all the song lyrics and creating a features matrix we were left with an array containing 30,000 features.
We wanted to see how five basic models, **Multinomial Naive Bayes, Random Forest, AdaBoost, Gradient Boost, K-Nearest Neighbors***, with both stemmed and lemmatized words compare score results and pick lemmatizing over stemmatizing in our five models for future model optimization. The chart below shows our results:

![](https://github.com/Botafogo1894/Project3/blob/master/basic%205%20models.png)

We chose to go with **lemmed words** over stemmed words because every model consistently performed at least 1% better.

We decided to go with the top three models, **Multinomial Naive Bayes, Gradient Boost, and Random Forest**, for further model optimization.

Next thing we did was PCA where we ran a test on our data to see how many components would preserve 80% of the variation.
Then we ran **PCA with n_components = 1800** on our top three models to see if that improved performance. The graph below shows the result:

![](https://github.com/Botafogo1894/Project3/blob/master/PCA%20for%20part%201.png)

As you can see from the graph, PCA didn't improve performance in either model, so we decided to not use PCA moving forward.

Next things we wanted to do was **GridSearch** on the three top-performing models and pick the model with the combination of parameters that yielded the highest accuracy score.

**GridSearch on the Random Forest** improved performance from **41% to 43%** accuracy.

**GridSearch on the Gradient Boost** improved performance from **45% to 50%** accuracy.

**GridSearch on Naive Bayes** did not generate improved performance because the default parameters are optimal.

## Interpreting and communicating the final results:

Below you can see the graph of our top three models Final Performance after optimization.

![](https://github.com/Botafogo1894/Project3/blob/master/top%203%20models.png)


