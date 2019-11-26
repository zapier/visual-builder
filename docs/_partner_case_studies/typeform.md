---
title: Typeform
order: 7
layout: post
redirect_from: /_partner_case_studies/
---

# Typeform

## Partner Profile

- **Product:** Online form builder and form creator
- **Founded:** 2012
- **Size:** 200-250 employees

## Integration Outcomes

We partnered with our friends at [Typeform](http://typeform.com) to validate the proclamation of the Zapier Developer Platform: "Make your app stickier than honey." That is, when an app integrates with Zapier (in effect, integrating with [over 400 other apps]()), the company's churn will decrease. Typeform was generous enough to share data with you and us to help figure out the answer.

### How the integration works

For a Typeform user to take advantage of the Zapier integration they need to go no further than the "Configure" step when setting up a form inside Typeform. There they find an option for "Integrations," at which point they're presented with the following options:

![Typeform's integration library powered by Zapier](
https://zapier.cachefly.net/storage/photos/3e56ea81261edd1215f12d9a70b89f7f.png)

## Do Typeform Users Churn Less with Zapier?

Typeform provided us data for 3,931 Typeform PRO users. 439 of those users also used Zapier. This gives a good base to analyze churn rates of the those who use just Typeform and those the use Typeform and Zapier together.

First lets define churn: in this case churn happens when a Typeform user downgrades from the $25/mo PRO plan to a free Typeform plan. However, some users may start out as just Typeform PRO users then later use Zapier in combination with Typeform. Those users churn rates should affect both cohorts (Typeform only, Typeform and Zapier).

With the two cohorts and churn rate well-defined, we can then look at the survival rates of both cohorts.

For those unfamiliar, survival curves represent the share of some sample or population that remains over time. By definition survival curves are always declining (or flat) as attrition is the rule.  For this reason, survival curves are commonly used in medical studies for diseases, hence the use of the word survival. 

This survival curve start at 100% with all users in an upgraded state. This represents the beginning of a user's time as a Typeform paid user. Throughout time (moving to the right on the chart) users churn and the survival curve decreases (moving down on the chart). The curves below are estimates based on the Cox Model (see the Methods section for details) with 95% confidence intervals shown as dashed lines.

![](https://zapier.cachefly.net/storage/photos/2027d88fabe1d3328c7e71661872341d.png)

Subtracting the survival curve from 100% (flipping it), yields curves that represent churn, take a look:

![](https://zapier.cachefly.net/storage/photos/3fc529b53830d5bde37c8c6a175ed2aa.png)

Overall, Typeform's churn curve resembles that of a typical SaaS business. Generally, payment dates that occur each month are where cancellations and churn cluster. After 1 year of usage, 75% of the beginning set of monthly subscribers is still with us, while 25% have churned at some point during the year. This is not to be confused with the typical monthly calculation of churn (churning users /  users active at the beginning of month) or similar churn calculations. Those calculations include a mix of customers, both new and long-time customers, and are a time-series.

The difference is clear, those that use Zapier and Typeform together have a lower rate of churn than those that just use Typeform. We should be clear, this is not a randomized study and it would not be honest to claim Zapier <i>causes</i> lower churn in partners. Rather, we suspect that Typeform users seeking to integrate with other apps are also likely to be those that find the most value in Typeform, and Zapier is a conduit to that end.

## Methods

Estimates of survival curves can be obtained by estimating any one of four other functions: probability density function, cumulative density function, cumulative hazard function, or a hazard function. A variety of methods exist for estimating each of these forms of survival behavior, but for our purposes estimating the hazard function is the most convenient.  This is because we're including a time-varying coefficient in the sense that we're allowing for staggered adoption of Zapier in the model. Below are relationships between the various incarnations of survival:

![](https://zapier.cachefly.net/storage/photos/54da96685cec3ce644bc2dcacb36c28c.png)

Two separate regression models were used to assess the difference in churn between the two groups.  Both a Cox Proportional Hazard model (“Cox Model”) and Aalen Additive Model (“Aalen Model”) were fit to the data.  The Cox Model is a semi-parametric model of the form:

![](https://zapier.cachefly.net/storage/photos/68f38c3b7b35698bc9f33032b837e588.png)

The Cox Model yields a distribution-free test for the equality of distributions when the distributions have roughly proportional hazard functions (Lawless 2002).  Inspection of residuals supports this assumption.  The Aalen Model also allows for time-dependent hazard rates and [serves as a complement to the Cox Model](http://www.ncbi.nlm.nih.gov/pubmed/22393999) that does not rely on the assumption of proportional hazards.  The Aalen Model is specified as: 

![](https://zapier.cachefly.net/storage/photos/a194b70e1f33cb517d6852c63898a72a.png)

Estimates from the Aalen Model mirror the difference in hazard rates between users that use Typeform as compared to those that use both Typeform and Zapier together. The survival and cumulative density functions shown in the graphs above are derived from estimates of the hazard function.

## Our Conclusions

Test statistics from both the Cox and Aalen Models provide evidence that the difference is unlikely to be due to random chance.  Given that there is a large amount of data, with almost 4,000 users included in the dataset, this is no surprise.  What matters most is that the curves are also meaningfully different for the business.

Typeform itself clearly returns a lot of value to its PRO customers, with only 1 in 4 paid customers downgrading over a year. With Zapier part of the picture though, that figure is about 1 in 6 customers.

Said another way, if churn of Typeform PRO users is the baseline, those that also use Zapier have churn of about 60% of the baseline.

We'd love to run similar analyses with our other integration partners to build that evidence. Interested in teaming up with Zapier for an analysis?
<p style="text-align:center"><a class="pill-button mongo orange" style="margin: 10px;" href="mailto:chris.peters@zapier.com">Shoot me an email!</a></p>

Or if you're not yet integrated with Zapier, please visit the [Zapier Developer Platform](https://zapier.com:443/platform) to learn more.

## References

- Abadi, Alireza, et al. "Comparison of Aalen’s additive and Cox proportional hazards models for breast cancer survival: analysis of population-based data from British Columbia, Canada." Asian Pacific Journal of Cancer Prevention 12 (2011): 3113-3116.
- Lawless, J. F. (2002) Statistical Models and Methods for Lifetime Data, Second Edition, John Wiley & Sons, Inc., Hoboken, NJ, USA. doi: 10.1002/9781118033005
- Meeker, William Q. and Luis A. Escobar (1998) Statistical Methods for Reliability Data, John Wiley & Sons, Inc., Hoboken, NJ, USA. ISBN: 978-0471143284

*Explore how you could succeed with Zapier like Paperform—get in touch with us at [partners@zapier.com](mailto:partners@zapier.com).*
