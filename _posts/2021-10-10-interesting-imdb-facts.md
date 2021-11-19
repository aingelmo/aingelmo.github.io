---
title: Interesting IMDB facts
layout: post
post-image: "https://images.pexels.com/photos/265685/pexels-photo-265685.jpeg"
description: Have you ever wondered what's the most expensive movie ever made? In this post, you may find interesting answers.
tags:
- pandas
- jupyter notebook
- data analysis
---

[IMBd](https://imdb.com){:target="_blank"} is the biggest source of information regarding movies in the world. By analyzing its whole database, we can get some insights in very interesting matters. For example, have you ever wonder what is the most popular genre over the years? Are the new movies more profitable than older ones? Find the answers to all your questions in this post!

# Dataset
The dataset used for the analysis contains information from more than 10k movies from the well-known website "IMDb". The dataset columns give information regarding to popularity, genres, revenue, budget and release year among others. It is structured in the following way:
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 10866 entries, 0 to 10865
Data columns (total 21 columns):
 #   Column                Non-Null Count  Dtype  
---  ------                --------------  -----  
 0   id                    10866 non-null  int64  
 1   imdb_id               10856 non-null  object 
 2   popularity            10866 non-null  float64
 3   budget                10866 non-null  int64  
 4   revenue               10866 non-null  int64  
 5   original_title        10866 non-null  object 
 6   cast                  10790 non-null  object 
 7   homepage              2936 non-null   object 
 8   director              10822 non-null  object 
 9   tagline               8042 non-null   object 
 10  keywords              9373 non-null   object 
 11  overview              10862 non-null  object 
 12  runtime               10866 non-null  int64  
 13  genres                10843 non-null  object 
 14  production_companies  9836 non-null   object 
 15  release_date          10866 non-null  object 
 16  vote_count            10866 non-null  int64  
 17  vote_average          10866 non-null  float64
 18  release_year          10866 non-null  int64  
 19  budget_adj            10866 non-null  float64
 20  revenue_adj           10866 non-null  float64
dtypes: float64(4), int64(6), object(11)
```

# Exploratory data analysis
Usually, when performing an analysis, starting with an histogram is a good idea. By doing this, we can get very helpful insights regarding the dataset.

![imdb-hist](/assets/images/imdb-facts/imdb_histogram.png)

From this histogram we can get two obvious facts: a lot of new movies have been made in the last twenty years and the average vote results is around 6. But let's do a more profound analysis.

## How many movies have been done over the years?
It is nice to begin our analysis detailing the previous exposed fact. Taking a look at the following graph, we can notice that the movie industry has skyrocketed in the past twenty years. 

![imdb-movies-count](/assets/images/imdb-facts/imdb_movies_count.png)

More and more movies are being done. The sector is booming but, are all of them profitable? Let's find out.

## What are the most expensive movies ever made?
At this point you may be wondering what is the most expensive movie ever made and our dataset allow us to do that. 

|      | original_title                              | release_date   | director       |   budget_adj |   revenue_adj |
|-----:|:--------------------------------------------|:---------------|:---------------|-------------:|--------------:|
| 2244 | The Warrior's Way                           | 12/2/10        | Sngmoo Lee     |  4.25e+08    |   1.10876e+07 |
| 3375 | Pirates of the Caribbean: On Stranger Tides | 5/11/11        | Rob Marshall   |  3.68371e+08 |   9.90418e+08 |
| 7387 | Pirates of the Caribbean: At World's End    | 5/19/07        | Gore Verbinski |  3.15501e+08 |   1.01065e+09 |
| 6570 | Superman Returns                            | 6/28/06        | Bryan Singer   |  2.92051e+08 |   4.2302e+08  |
| 5231 | Titanic                                     | 11/18/97       | James Cameron  |  2.71692e+08 |   2.50641e+09 |

**The Warrior's Way**, an action/fantasy film by the korean director Lee Seung-moo in 2010 seems to be the highest budgeted movie in history. However, it is not. Someone added an extra 0 when inputing the data and made it look like the highest budgeted movie ever with 420,000,000 $. The correct amount is 42,000,000 $.

Knowing that, the second in place must be the highest budgeted movie in history: **Pirates of the Caribbean: On Stranger Tides** by american director Rob Marshall. It costed the incredible amount of 360,000,000 $. It also seems that Pirate of the Caribbean saga is quite costly because the third most expensive movie ever is **Pirates of the Caribbean: At World's End** by amercan director Gore Verbinski.

This movies are super expensive but, are they really the ones that get the most revenue? We'll find out.

## What are the highest-grossing films ever made?
It is nice to know the most expensive movies ever made but, what about the highest-grossing ones?

|       | original_title   | release_date   | director         |   budget_adj |   revenue_adj |
|------:|:-----------------|:---------------|:-----------------|-------------:|--------------:|
|  1386 | Avatar           | 12/10/09       | James Cameron    |  2.40887e+08 |   2.82712e+09 |
|  1329 | Star Wars        | 3/20/77        | George Lucas     |  3.95756e+07 |   2.78971e+09 |
|  5231 | Titanic          | 11/18/97       | James Cameron    |  2.71692e+08 |   2.50641e+09 |
| 10594 | The Exorcist     | 12/26/73       | William Friedkin |  3.92893e+07 |   2.16732e+09 |
|  9806 | Jaws             | 6/18/75        | Steven Spielberg |  2.83627e+07 |   1.90701e+09 |

**Avatar**, a movie directed by James Cameron and released in 2007, is the highest grossing movie with more than 2.8 billion dolars in box office. But this is not the only James Cameron movie in the top 5! _Titanic_, released in 1997, was also directed by him! What a guy! 

There are other well-known movies on the list like _Star Wars_ by George Lucas or _Jaws_ by Steven Spielberg. 

Another important insight we may find is that three out of the five highest-grossing films ever made were done in the 1970s. Maybe people had less leisure options back then.

Now we know the movies that made the highest box office in history but some may be interested in knowing the profit. Because, yes, you can earn a lot but, if you cost a lot... that isn't great news.

## What are the most profitable movies ever made?
Profitability can be measured in a variety of ways. It can be absolute or relative. In absolute terms, super productions will have an advantage because they are made to sell a lot. Let's check it out.

|       | original_title   | release_date   | director         |   budget_adj |   revenue_adj |   profit_adj |
|------:|:-----------------|:---------------|:-----------------|-------------:|--------------:|-------------:|
|  1329 | Star Wars        | 3/20/77        | George Lucas     |  3.95756e+07 |   2.78971e+09 |  2.75014e+09 |
|  1386 | Avatar           | 12/10/09       | James Cameron    |  2.40887e+08 |   2.82712e+09 |  2.58624e+09 |
|  5231 | Titanic          | 11/18/97       | James Cameron    |  2.71692e+08 |   2.50641e+09 |  2.23471e+09 |
| 10594 | The Exorcist     | 12/26/73       | William Friedkin |  3.92893e+07 |   2.16732e+09 |  2.12804e+09 |
|  9806 | Jaws             | 6/18/75        | Steven Spielberg |  2.83627e+07 |   1.90701e+09 |  1.87864e+09 |

Based on the previous list, **Star Wars** is the most profitable movie of all time. We can also see that the other four movies on the list are super productions like _Avatar_ or _Titanic_. But, how about smaller productions. Can we measure its impact in the industry? Of course we can! By calculating the profit in relative terms. This means, how much they raised in proportion o what they costed.

|      | original_title          | release_date   | director                       |   budget_adj |   revenue_adj |   profit_adj |   profit_rel_adj |
|-----:|:------------------------|:---------------|:-------------------------------|-------------:|--------------:|-------------:|-----------------:|
| 7447 | Paranormal Activity     | 9/14/07        | Oren Peli                      |      15775   |   2.03346e+08 |  2.0333e+08  |        12889.4   |
| 2449 | The Blair Witch Project | 7/14/99        | Daniel Myrick                  |      32726.3 |   3.24645e+08 |  3.24612e+08 |         9919     |
| 1354 | Eraserhead              | 3/19/77        | David Lynch                    |      35977.8 |   2.51845e+07 |  2.51485e+07 |          699     |
| 7277 | Pink Flamingos          | 3/12/72        | John Waters                    |      62574.7 |   3.12874e+07 |  3.12248e+07 |          499     |
| 7178 | Super Size Me           | 1/17/04        | Morgan Spurlock                |      75039   |   3.29884e+07 |  3.29133e+07 |          438.617 |

In this list, **Paranormal Activity**, a horror movie directed by Oren Peli released in 2007 appears at the first place. However, its profit is way less than _Star Wars_ or _Avatar_. How can this be possible? Well, _Paranormal Activity_ budget was only 15,000 dolars and it raised more than 200,000,000 dolars in revenue. This is huge! It raised more than 12,500 times its budget in revenue. Incredible.

Taking a look at the list, we may find some other interesting insights. _The Blair Witch Project_ and _Eraserhead_ are also horror movies. Seems like this genre is very profitable!

## What are the biggest deceptions in history?
Not all the movies are good. Some of them have a very high budget but perform badly in box office. We call this a deception. Let's take a look at the movies with the worst profit in history.

|      | original_title    | release_date   | director                   |   budget_adj |   revenue_adj |   profit_adj |
|-----:|:------------------|:---------------|:---------------------------|-------------:|--------------:|-------------:|
| 2244 | The Warrior's Way | 12/2/10        | Sngmoo Lee                 |  4.25e+08    |   1.10876e+07 | -4.13912e+08 |
| 5508 | The Lone Ranger   | 7/3/13         | Gore Verbinski             |  2.38689e+08 |   8.35783e+07 | -1.5511e+08  |
| 7031 | The Alamo         | 4/7/04         | John Lee Hancock           |  1.67395e+08 |   2.98077e+07 | -1.37587e+08 |
| 2435 | The 13th Warrior  | 8/27/99        | John McTiernan             |  2.09448e+08 |   8.07671e+07 | -1.28681e+08 |
| 4970 | Brother Bear      | 10/20/03       | Aaron Blaise|Robert Walker |  1.18535e+08 | 296.338       | -1.18535e+08 |

Again, _The Warrior's Way_ appears to be the worst. However, we know that the budget is not correct so let's move to the second. **The Lone Ranger**, released by Disney in 2013 is the worst movie ever in economic terms. It made the studio lose more than 150,000,000 dolars. That is a huge loss!

Taking a deeper look into the table we find a interest fact. All of the movies were super expensive, costing more than 100,000,000 dolars. It looks like super productions can turn in a studio's biggest enemy.

## Are more popular movies more profitable?
A common assumption to think is that more popular movies should gross higher revenue. However, does this relate to profit? In the following graph we can see a relation between profit a popularity.

![imdb-popularity-profit](/assets/images/imdb-facts/imdb_popularity_profit.png)

Taking a look at the graph above, we may conclude that more popular movies tend to be more profitable and it makes sense. More popular movies have a higher change of grossing a higher revenue, the more revenue a movie raise, the more potential it has to become profitable.

## What is the average vote rating?
Another important insight we can get from the data is the average vote rating from users. This would allow us to know if a movie is above the average or below. If a movie rating is higher than the median, the chances of it being good are higher than if the rate is lower.

![imdb-movies-rating](/assets/images/imdb-facts/imdb_movies_rating.png)

Based on the previous histogram, we can conclude that most of the movies are rated near 6. Let's detail it.

|       |   vote_average |
|:------|---------------:|
| count |       10725    |
| mean  |       5.96432  |
| std   |       0.930166 |
| min   |       1.5      |
| 25%   |       5.4      |
| 50%   |       6        |
| 75%   |       6.6      |
| max   |       9.2      |

The median is exactly 6. This means that 50% of movies are above 6 and 50% below 6. The highest rated movie in the dataset is 9.2 while the lowest is 1.5. We also may say that a movie with a rating above 6 has higher chances of being good.

## Are newer movies worst than old ones?
This is another question that may arise. Ok, we know the average rating of movies but, are the new ones worst rated? Let's find out. The following groups the movies newer than 2006 (included) and older than 2006. 

![imdb-movies-rating-old-new.png](/assets/images/imdb-facts/imdb_movies_rating_old_new.png)

The graph shows that old movies are slightly better rated than new movies. However, the difference is noth enough to affirm that old movies are better than new movies.

# Conclusion

I could be exposing insights regarding this dataset. However, the post is getting to long so I will stop there. **If you are interested in knowing more about movies and the procedures used to clean and draw conclusions, please take a look at [my jupyter notebook](https://github.com/aingelmo/portfolio/blob/main/Udacity/Project_2_Investigate%20a%20Dataset/investigate-a-dataset-template.ipynb){:target="_blank"}.**

After analyzing the dataset, we may conclude the following:
*   Lots of movies are being done nowadays. However, this doesn't imply that all of them are profitable. The probabily of failing is as high as succeeding. _Avatar_, released in 2009, is the highest-grossing movie of all time and second most profitable. However, _The Lone Ranger_, released in 2013, is the worst profitable movie of all times. Studios shold be careful when releasing movies nowadays as people have more leisure activity options than 40 years ago.
*   Horror movies seems to perform well in terms of yield. _Paranormal Activity_ multiplied its budget by more than 12,000 times in revenue. This is a huge success, as well as _The Blair Witch Project_ and _Eraserhead_.
*   Older movies are better rated than newer ones. In the old days, as less movies were made, it was easier to make a good movie. However, nowadays the probability of making a bad movie is higher as the amount of movies has increased a lot.

Thank you for reading until the end. Hope you enjoyed it!