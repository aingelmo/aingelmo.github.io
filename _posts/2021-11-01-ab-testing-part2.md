---
title: Should I deploy my new website? Or better keep the old one? (Part 2 - Z-test)
layout: post
post-image: "https://images.pexels.com/photos/590022/pexels-photo-590022.jpeg"
description: A/B tests are very commonly performed by data analyst. In this post, I'll run some tests to help a fake company understand if they should implement the new page or keep the old one.
tags:
- pandas
- jupyter notebook
- data analysis
- A/B test
- probability
- statsmodels

---

In the [last post](https://aingelmo.github.io/blog/ab-testing-part1){:target="_blank"}, we tried to perform an A/B test for a website in order to deploy a new website or not. However, all the calculations were done in a 'manual' way. Python offers us the possibility to use built-ins to achieve similar results. This built-ins are easier to code.

## Calculations

We will use **statsmodel** module to perform the same A/B test than before.

First, let's count the converted users by the landing page that converted them:

```python
convert_old = df2.query('landing_page == "old_page" & converted == 1').shape[0]
convert_new = df2.query('landing_page == "new_page" & converted == 1').shape[0]
n_old = df2[df2["landing_page"] == "old_page"].shape[0]
n_new = df2[df2["landing_page"] == "new_page"].shape[0]
```

The data goes as follows:

$$convert_{old} = 17489$$

$$convert_{new} = 17264$$

$$n_{new} = 145310$$

$$n_{old} = 145274$$

After getting the number of converted people and the population based on the landing page, we can perform a ztest to compute the test statistic and the p-value:

```python
from statsmodels.stats.proportion import proportions_ztest

counts = np.array([convert_old, convert_new])
nobs = np.array([n_old, n_new])

stat, pval = proportions_ztest(counts, nobs, alternative='smaller')
```

where:

* `counts` is the number of successes in nobs observations.
* `nobs` is the number of observations.
* `alternative` is the the kind of hypothesis testing we are doing. In this case, we want to know if $$H_{1}$$ performs better than $$H_{0}$$ so we will select `smaller`.

The data thrown by the proportion z_test is the following:

$$stat = 1.3109241984234394$$

$$pval = 0.9050583127590245$$

## Conclusion

The $$stat$$ equals to 1.31 which translates to a $$pval$$ is 0.90. This is higher than our error 1 margin rate ($\alpha$) of 0.05 that we set on the beginning. This means that we do not have enough evidence to reject the null. In other words, we cannot say, based on the data we have, that the new website provides more conversions than the old one.
