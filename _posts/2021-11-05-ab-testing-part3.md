---
title: Should I deploy my new website? Or better keep the old one? (Part 3: Logistic Regression)
layout: post
post-image: "https://images.pexels.com/photos/590022/pexels-photo-590022.jpeg"
description: A/B tests are very commonly performed by data analyst. In this post, I'll run some tests to help a fake company understand if they should implement the new page or keep the old one.
tags:
- pandas
- jupyter notebook
- data analysis
- A/B test
- probability
- statsmodel

---

## Introduction

This is the last post of the A/B test series. You can check part 1 [here](https://aingelmo.github.io/blog/ab-testing-part1){:target="_blank"} and part 2 [here](https://aingelmo.github.io/blog/ab-testing-part2){:target="_blank"}. In this part, I will take a regression approach. More precisely, a logistic regression.

## Calculations

A logistic regression takes values between 0 an 1. The goal is to use **statsmodels** to fit the regression and see if there is a significant difference in conversion based on which a page a customer receives. But first, we need to calculate a column for the intercept, in which the values are equal to one, and a  ab_page column, which is 1 when an individual receives the treatment and 0 if control.

```python
df["intercept"] = 1
df[["ab_page"]] = pd.get_dummies(df2["group"], drop_first=True)
```

We will use `statsmodel.Logit` to build the regression model and then fit the results.

```python
lm = sm.Logit(df["converted"], df[["intercept", "ab_page"]])
results = lm.fit()
```

The results are as followed:

```text
                          Results: Logit
==================================================================
Model:              Logit            Pseudo R-squared: 0.000      
Dependent Variable: converted        AIC:              212780.3502
Date:               2021-11-05 11:55 BIC:              212801.5095
No. Observations:   290584           Log-Likelihood:   -1.0639e+05
Df Model:           1                LL-Null:          -1.0639e+05
Df Residuals:       290582           LLR p-value:      0.18988    
Converged:          1.0000           Scale:            1.0000     
No. Iterations:     6.0000                                        
-------------------------------------------------------------------
              Coef.   Std.Err.      z      P>|z|    [0.025   0.975]
-------------------------------------------------------------------
intercept    -1.9888    0.0081  -246.6690  0.0000  -2.0046  -1.9730
ab_page      -0.0150    0.0114    -1.3109  0.1899  -0.0374   0.0074
==================================================================
```

In this case, $$pval = 0.1899$$. In the previous parts, $$pval = 0.9050$$. Why is this happening?

### New model hypothesis

In part 1 and part 2, the hypotheses for our model were:

$$H_0: p_{new} - p_{old} <= 0$$

$$H_1: p_{new} - p_{old} > 0$$

However, in the new one, the hypotheses are:

$$H_0: p_{new} = p_{old}$$

$$H_1: p_{new} \neq p_{old}$$

In other words, in the first two parts, we wanted to compare if the new page could perform better than the old one. To do that, we assumed that the new page would perform equal or worse than the old one and we failed to reject it.

In this model, we are performing a two-tail test. We would assume that the new page performs as good as the old one and we would like to reject it. We would like to know if there is a differences in conversions between both pages.

However, the model is pretty incomplete. We cannot estimate the outcome precisely based on just one observation. This is why we are going to add another variables.

### New added variables

Adding more factors to the regression model may predict the outcome better. However, we may incur in multicolinearity. This means that the factors we are including in our model are correlated. To solve this, we would have to run a VIF test and check that the values were below 10.

The first few observations of the new table looks like this:

|    |   user_id | country   |
|---:|----------:|:----------|
|  0 |    834778 | UK        |
|  1 |    928468 | US        |
|  2 |    822059 | UK        |
|  3 |    711597 | UK        |
|  4 |    710616 | UK        |

We have to merge them with the old table and retrieve the dummies. The new dataframe would look like this:

|    |   user_id | timestamp                  | group     | landing_page   |   converted |   intercept |   ab_page | country   |   CA |   UK |   US |
|---:|----------:|:---------------------------|:----------|:---------------|------------:|------------:|----------:|:----------|-----:|-----:|-----:|
|  0 |    851104 | 2017-01-21 22:11:48.556739 | control   | old_page       |           0 |           1 |         0 | US        |    0 |    0 |    1 |
|  1 |    804228 | 2017-01-12 08:01:45.159739 | control   | old_page       |           0 |           1 |         0 | US        |    0 |    0 |    1 |
|  2 |    661590 | 2017-01-11 16:55:06.154213 | treatment | new_page       |           0 |           1 |         1 | US        |    0 |    0 |    1 |
|  3 |    853541 | 2017-01-08 18:28:03.143765 | treatment | new_page       |           0 |           1 |         1 | US        |    0 |    0 |    1 |
|  4 |    864975 | 2017-01-21 01:52:26.210827 | control   | old_page       |           1 |           1 |         0 | US        |    0 |    0 |    1 |

The new regression model would look like:

```text
                          Results: Logit
==================================================================
Model:              Logit            Pseudo R-squared: 0.000      
Dependent Variable: converted        AIC:              212781.1253
Date:               2021-11-05 12:11 BIC:              212823.4439
No. Observations:   290584           Log-Likelihood:   -1.0639e+05
Df Model:           3                LL-Null:          -1.0639e+05
Df Residuals:       290580           LLR p-value:      0.17599    
Converged:          1.0000           Scale:            1.0000     
No. Iterations:     6.0000                                        
-------------------------------------------------------------------
              Coef.   Std.Err.      z      P>|z|    [0.025   0.975]
-------------------------------------------------------------------
intercept    -1.9893    0.0089  -223.7628  0.0000  -2.0067  -1.9718
ab_page      -0.0149    0.0114    -1.3069  0.1912  -0.0374   0.0075
CA           -0.0408    0.0269    -1.5161  0.1295  -0.0934   0.0119
UK            0.0099    0.0133     0.7433  0.4573  -0.0162   0.0359
==================================================================
```

Now we have the coefficients, taking United States as reference, we can know how users coming from Canada or United Kingdom. However, we cannot say that Canada users have a 0.04% less chance of being converted with the new website, we have to convert the coefficients before:

$$$e^{UK} = 1.01$$$

$$$e^{CA} = 0.96$$$

We can say that users from United Kingdom would be 1.01 times more likely of being converted than people from the United States. On the other hand, users from Canada would be 0.96 times less likely of being converted than users from the US.

Though we have looked at the individual factor of country and page on conversions, we would like to know if there is a significant effect on conversion. Let's create two new columns:

```python
df["UK_ab_page"] = df["ab_page"] * df["UK"]
df["CA_ab_page"] = df["ab_page"] * df["CA"]
```

The first few observations of the new dataframe would look like this:

|    |   user_id | timestamp                  | group     | landing_page   |   converted |   intercept |   ab_page | country   |   CA |   UK |   US |   UK_ab_page |   CA_ab_page |
|---:|----------:|:---------------------------|:----------|:---------------|------------:|------------:|----------:|:----------|-----:|-----:|-----:|-------------:|-------------:|
|  0 |    851104 | 2017-01-21 22:11:48.556739 | control   | old_page       |           0 |           1 |         0 | US        |    0 |    0 |    1 |            0 |            0 |
|  1 |    804228 | 2017-01-12 08:01:45.159739 | control   | old_page       |           0 |           1 |         0 | US        |    0 |    0 |    1 |            0 |            0 |
|  2 |    661590 | 2017-01-11 16:55:06.154213 | treatment | new_page       |           0 |           1 |         1 | US        |    0 |    0 |    1 |            0 |            0 |
|  3 |    853541 | 2017-01-08 18:28:03.143765 | treatment | new_page       |           0 |           1 |         1 | US        |    0 |    0 |    1 |            0 |            0 |
|  4 |    864975 | 2017-01-21 01:52:26.210827 | control   | old_page       |           1 |           1 |         0 | US        |    0 |    0 |    1 |            0 |            0 |

And the new regression would look like this:

```text
==================================================================
Model:              Logit            Pseudo R-squared: 0.000      
Dependent Variable: converted        AIC:              212782.6602
Date:               2021-11-26 13:35 BIC:              212846.1381
No. Observations:   290584           Log-Likelihood:   -1.0639e+05
Df Model:           5                LL-Null:          -1.0639e+05
Df Residuals:       290578           LLR p-value:      0.19199    
Converged:          1.0000           Scale:            1.0000     
No. Iterations:     6.0000                                        
-------------------------------------------------------------------
              Coef.   Std.Err.      z      P>|z|    [0.025   0.975]
-------------------------------------------------------------------
intercept    -1.9865    0.0096  -206.3440  0.0000  -2.0053  -1.9676
ab_page      -0.0206    0.0137    -1.5052  0.1323  -0.0473   0.0062
CA           -0.0175    0.0377    -0.4652  0.6418  -0.0914   0.0563
UK           -0.0057    0.0188    -0.3057  0.7598  -0.0426   0.0311
CA_ab_page   -0.0469    0.0538    -0.8718  0.3833  -0.1523   0.0585
UK_ab_page    0.0314    0.0266     1.1807  0.2377  -0.0207   0.0835
==================================================================
```

The  converted coefficients:

$$$e^{UK_ab_page} = 1.032$$$

$$$e^{CA_ab_page} = 0.954$$$

$$$e^{UK} = 0.994$$$

Now we can know if the new page is working for the different countries. In this case, taking US as the base, the UK users will be 1.032 times more likely of being converted when landing in the new page. On the other hand, CA users will 0.954 times less likely of being converted when landing in the new page.

The most interesting factor here is that, holding everything constant, UK users would be a little less likely (0.994) than US users of being converted when considering both landing pages. However, when UK users land in the new website, the likelihood of them being converted increases in 1.032 times than US users landing in the new website.

## Conclusions

We can say that logistic regressions suit A/B testing. However, it is really important to add as much relevant variables as we can to get more precise results. In this case, when adding the countries information, we could conclude that, depending on the country, the landing website has an impact on conversions.

Despite being very little, when the amount of users is high, being 1.03 times more likely to convert the user does have an impact. More precisely, in the UK, the new website seems to be working better than the old ine. For others, like CA, the old one may work better than the new one.

**For a more detailed explanation, please, consider taking a look to the Jupyter Notebook associated to this project on [my GitHub](https://github.com/aingelmo/portfolio/blob/main/Udacity/Project_3_Analyze%20AB%20Test%20Results/Analyze_ab_test_results.ipynb)**
