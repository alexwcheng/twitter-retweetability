# Twitter Business

![Title_Slide](/Images/Slides/Title_Slide.png)

#
### Project File Summary

   - <b>[README.md](README.md)</b> - a summary of all contents in this repository.
   - <b>[/Data](/Data)</b> - All data called from the Twitter API.
   - <b>[/Images](/Images)</b> - Exported plots, etc...
   - <b>[/Jupyter_Notebooks](/Jupyter_Notebooks)</b> - All Jupyter Notebooks for this project.
   - <b>[/Project_Prompt](/Project_Prompt)</b> - The prompt for this project.
   - <b>[/Python_Files](/Python_Files)</b> - .py files loaded / imported in the Jupyter Notebooks.
   - <b>[/Final_Presentation](/Final_Presentation)</b> - A non-technical presentation of our project.

#
### Project Members

   - <b>[Alex Cheng](https://github.com/alexwcheng)</b>
   - <b>[Stuart Murphy](https://github.com/thespud56)</b>
   
#
### Project Responsibilities

   -  All project responsibilities were shared equally between <b>[Alex Cheng](https://github.com/alexwcheng)</b> and <b>[Stuart Murphy](https://github.com/thespud56)</b>.

#
### Project Scenario

Our client is a FinTech company looking to scale their customer acquisition efforts. They know that their target market are people who care deeply about their finances, and actively discuss finances in their everyday lives. They are also tech-savvy and are open to trying new digital & mobile experiences when interacting with their money (early adopters). Our client wishes to use their marketing budget wisely. They are aware that the best kind of marketing is 'word of mouth' marketing and want to produce content that will most likely get shared and retweeted by their followers. An example client might be a financial tech company like Alluva with only a few thousand followers, as seen below.

![Fintech_Example_Twitter_User](/Images/Slides/Fintech_Example_Twitter_User.png)

#
### Project Goals

The goal of this project is to help our client identify **the most important attributes** around a tweet and a twitter user that will lead to the most retweets. Our target (dependent variable) is the **number of retweets,** split into 3 classes:
1. **0-100 Retweets**
2. **100-1000 Retweets**
3. **1000+ Retweets**

#
### Data

Our dataset comes from the [Twitter API](https://developer.twitter.com/en/docs/api-reference-index), using 3 endpoints: 
1. **Users**
2. **Tweets**
3. **Tweet Details (Deets)**

We decided on **10 terms** targeting **Financial Tech (Fintech)** that we used to retrieve tweets that are most related to Fintech news, products, and services. We decided to collect up to **5,000 tweets per query term.** Sometimes, the number of results ran out before we reached 5,000 tweets for a particular query term. 

![Fintech_Twitter_Query_Terms](/Images/Slides/Fintech_Twitter_Query_Terms.png)

The data collection process required a large number of API requests via token pagination at 100 results per request. After collecting all of the tweet data (Tweets), the user ids and tweet ids were harvested, and used to request user information (Users) and detailed tweet metrics (Deets) for each collected tweet. All of this data was cleaned, transformed into the most appropriate datatypes, and merged into one dataframe.

Next, we needed to filter the data. A confounding aspect of our dataset is that we are getting tweets from users with a wide range of follower counts. Of course, follower count and retweets are correlated. As more people follow an account, the account generally gets more attention. For example, if an influencer tweets about something fintech related, versus an average Joe, obviously the influencer's post would be retweeted more. We wanted to eliminate this effect as much as possible in our study. **To control for this, we only considered tweets by users that have a follower count similar to a startup company. Based on our research, this is somewhere between 1,000 and 10,000 followers.**

This filtering process reduced our dataset from nearly 40,000 tweets to roughly 12,000 tweets, but still left us a decent chunk of data to work with. 

#
### Predictor Variables

![Twitter_Features](/Images/Slides/Twitter_Features.png)

#
### Feature Engineering

We were curious if the text length in a user's bio, or the text length of a tweet had any part in predicting retweetability. So, we analyzed tweets by number of characters, to create two new features: "user description character length" and "tweet character length".

In addition, we generated new graphics-related categorical variables for prediction. Using one-hot-encoding, we created six new features using the 3 most popular "user profile text colors" and 3 most popular "user profile background colors" that we found in our dataset.

Most importantly, as part of the feature engineering process - we needed to create our dependent variable **"Retweet Class"** that we could use to make predictions. This allowed us to identify if a tweet had a high number of retweets (1000+), a moderate number of retweets (100 - 1000), or a low number of retweets (< 100).

At the end of the feature engineering process, we had **29 features**. (28 predictor variables and 1 target variable.)

### Data Preprocessing

Since we had lots of numerical data that is measured on different scales, it was important to **standardize** this data using StandardScalar. This standardization allows the model to train on a "level playing field", so that no one variable's numerical scale has an unfair advantage or disadvantage compared to the others as the model adjusts weights during training. We also used Scikit-learn to "Train, Test, Split" our data using an 80/20 split, which allowed us to train our model sufficiently before making predictions.

#
### Random Forest Model

We decided to use a **Random Forest** algorithm for modeling, for several reasons: 

1. Clear interpretability of feature importances was a priority. 
2. We had a lot of features to work with, and wanted to really just find the top 5 or 10 features that mattered most.
3. The dataset was not prohibitively large, therefore the computational cost of a Random Foreset model is not overbearing.

We trained the model using 80% of our dataset and performed hyperparameter tuning using RandomizedSearchCV with further refinement using GridSearchCV. The tuning process included the following hyperparameters: 

- max depth
- number of estimators
- max features
- min samples leaf
- min samples split
- bootstrapping 

We also performed cross-validation on our model to ensure our predictions on the training set wasn't an anomaly.

#
### Model Results

#
### Conclusions

#
### Future Work
