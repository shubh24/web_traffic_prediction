# web_traffic_prediction
Predicting traffic on Wikipedia pages -- A Kaggle competition

**Feature Engineering**

*Overall Mean/Median* -- A simple constant submission with the mean/median over the last 8 weeks turned out pretty tough to beat in Stage 1. Included them as features too. 

*Rolling means and rolling medians* -- These were some of the most obvious features that came to my head, however they weren't as simple to implement. Agreed, the rolling mean of the last 7 days would be an important feature while predicting today's traffic, but the challenge is asking us to predict the traffic data for the next three months. 

How'll you find the weekly rolling mean of 1st November, when the current date is 14th of September?

Thus, features like rolling mean performed really well in validation but not on the public leaderboard. Finally, i went ahead with rolling means and medians of the last 30 and 60 days. For dates where i couldn't calculate these features, i went ahead with the proxy of the last available calculated feature in the time series.

Later on, i included more features like rolling standard dev, rolling min/max etc.

*Weekday-based mean/median* -- These features turned out to be one of the most important ones! Well obviously, a lot of Wikipedia clicks are weekday/weekend-dependent -- i tried to capture that by taking the rolling weekday-aggregated mean and median over the last six months. 

*Language and Source* -- I tried incorporating statistics derived from the language of the page, or the source(Crawler, Spider etc), but those didn't get me a boost on a vanilla xgboost. Dropped them for the sake of simplicity. 

**Last day's visits** -- Features like the **last day's visits** were incredibly useful while doing a validation run. Not so with the testing data, because of the live nature of the competition. I have to submit predictions for all pages over the next two months -- Clearly, using last day's visits is stupid!
