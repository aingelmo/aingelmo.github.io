---
title: Analyzing WeRateDogs twitter profile
layout: post
post-image: "https://images.unsplash.com/photo-1546975490-a79abdd54533"
description: Do you want to know what is the cutest dog breed? And the most popular one? Let's take a look at the incredibly popular WeRateDogs.
tags:
- pandas
- jupyter notebook
- data analysis
- matplotlib
- twitter API
---

[WeRateDogs](https://twitter.com/dog_rates){:target="_blank"} is a incredibly popular Twitter account that rates people's dogs with humorous comments about the dog. The ratings usually have a denominator of 10. However, the numerator is almost always greater than 10. 11/10, 12/10, 13/10, etc. Why? Because dogs are cute and humans love them.

The dataset, gathered by Udacity, contains basic tweet data for more than 5,000 tweets posted by the profile. Despite this dataset being given to us by Udacity, it is not complete. We will have to complement it using the Twitter API.

The original dataset looks has more than 35 columns with data regarding the ID of the tweet, timestamp, text, rating, retweet count...

In this blog post however, we will be focusing in the conclusions extracted from the dataset. If you are intersted in the data wrangling part, please take a look at [this Jupyter Notebook](https://github.com/aingelmo/portfolio/blob/main/Udacity/Project_4_Wrange%20and%20Analyze%20Data/wrangle_act.ipynb){:target="_blank"}.

## Analysis

[WeRateDogs](https://twitter.com/dog_rates) joined twitter on November, 2015. Sinc then, they have been one of the most viral and active dog accounts on the platform but... have they always been so active? We can get a visual representation of **how WeRateDgos have been tweeting** along the timeframe analyzed.

![Tweets Histogram](assets\images\weRateDogs\tweet-histogram.png)

The graph above shows the amount of tweets posted by the account between November 15th, 2015 and August 1st 2017. As we can see, the distribution is right skewed. This means that more tweets weere posted in the early stages of the profile. Howvery, it could wrong to affirm that. It is only correct to say that, based on the dataset, more tweets were posted in the early stages of the account.

It is really interesting to know about the tweets frequency but you may be wondering, **what is the favourite dog breed for WeRateDogs?** We can answer this analyzing data from a neural network. This neural network analyzed each of the picture in WeRateDogs tweets and predicted its bread.

![Most Common Dog Breeds](assets\images\weRateDogs\most-common-breeds.png)

The most common dog breed identified by the algorithm is the golden retriever with almost 150 results. It is followed by the labrador retriever with 100 and the pembroke, also known as corgi, with 89 occurences.

But, can we say that the golden retriever is the most common dog breed posted by WeRateDogs? Of course not. We do not have enough evidence to support that hypothesis. The data we analyzed was from 2015 to 2017. Things can have changed. In the past, they could be biased when posting content about this type of dogs due to the fact that they could attract more audience, they looked more cute...

At this point, we know they like to post pictures of golden retrievers, labrador retrievers and corgis. Let's find out their **most popular tweet**. Their most reweetwed tweet is a [doggo realizing he can stand in the pool](https://twitter.com/dog_rates/status/744234799360020481){:target="_blank"}. How cool is that? It has almost 150,000 retweets by the time I am writing this!

However, not all the popular tweets can be measured in retweets, they can also be done in likes. This [little puppo supporting Toronto Womens March](https://twitter.com/dog_rates/status/822872901745569793){:target="_blank"} is the champion. More than 125K people have already like him. What are you waiting for?

To finish this analysis, I ran a test to know if **most popular breeds made the most popular tweets** and I was very surprised with the results. The golden retriever, chihuahua and labrador retriever made the top three. And this is not a coincidence. WeRateDgos knows what the people like, what we demand as consumers, and they deliver.

## Conclusions

WeRateDogs has been actived for quite a long time already. They know what the consumers like. They know our favourite breeds: labradors, goldens and corgis and the post about them. They know that the probabilities of going viral with of those breeds seems to be higher than other. It looks like they are succeeding with their posting method! Almost 10M followers and growing!

For more information regarding WeRateDogs profile analysis, data wrangling and more visualizations, please take a look at [my GitHub](https://github.com/aingelmo/portfolio/blob/main/Udacity/Project_4_Wrange%20and%20Analyze%20Data/wrangle_act.ipynb){:target="_blank"}. Thanks for reading until the end!

If you like my article. Please, consider reading another one from my [blog](https://aingelmo.github.io/blog){:target="_blank"} or checkout my [projects](https://aingelmo.github.io/project){:target="_blank"}.