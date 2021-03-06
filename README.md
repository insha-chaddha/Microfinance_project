
# Microfinance Project

Repository to look at access to microfinancing in India.

## Aims

Add information on aims for analysis here

## Limitations

| Problem                                    | Solution                                        |
|:------------------------------------------ |:----------------------------------------------- |
| Not enough data points. Once we remove people above the second lowest quintile, we’re left with approximately 900. records which is not enough for the analysis we would like to do.      | No solution to this. We can recognise the limitations of our analysis and ensure that the results are heavily caveated to take this into account.  |
| Not known whether people accessing financial services are doing so from a microfinance institution.| Examine literature in this field to assess whether there is any information collected so far on average income of account owner for MFI to deduce which income quintile they would fall under. We could use Mix Market data to predict this. |
| We only have snapshot data of someone’s banking journey, we cannot see how they might have been impacted by the introduction of microfinance services in their city/village. | No solution for this. We don’t have panel data which follows an individual through their life. However, we could use the 2017 data to see how banking journeys in aggregate have changed.|


### Notes

* The main analysis is held within an [Rmarkdown](https://rmarkdown.rstudio.com/articles_intro.html) document, Summarystats.Rmd.

Microfinance Summary Stats
================

This document is for general exploration of the India Findex 2014
dataset containing survey results from 3000 participants regarding their
financial habits.

# Introduction

### The objectives of microfinance institutions are:

  - To ensure everyone has access to financial services
  - To ensure that this access is provided fairly with due consideration
    given to their social circumstances
  - To provide the above services below the market price with a
    secondary aim of helping raise the living standards of those in
    lower income levels.

### Literature review

Within academic literature, evidence on the impact on household lifetime
wealth of microfinace services is mixed. Some studies such as Pitt and
Khandker (1998) found a statistically significant positive relationship
between a household’s use of credit and the value of the household
assets as well as the likelihood of the children attending school in
Bangladesh. However, when Knandker followed up with the subjects in the
original review and conducted a second set of surveys to examine
borrower behaviour over time, the relationship between credit and
markets of household lifetime wealth was greatly diminished. Other
studies such as Coleman (1999) examining microcredit in northern
Thailand also found no significant impact of credit access to household
wealth. However, Cotler and Woodruff (2017) found statistically
significant impacts of microlending on the sales and profit margins of
small businesses in Mexico.

In order to evaluate the impact of access to microfinace services in
isolation, studies must be able to control for sampling bias. Studies
such as Karlan and Zinman (2006) manage to do just that by collaborating
with a South African MFI to work with randomly chosen participants from
a cohort of clients who were on the borderline of loan approval but were
rejected. A random selection of these applicants were granted loans and
were surveyed both six months and twelve months later to observe the
impact of the loan. The researchers found that the chosen borrowers were
statistically significantly more likely to retain wage employment, less
likely to experience hunger in their household, and less likely to be
impoverished than their non-borrowing counterparts.

This report will examine the impact of interacting with financial
services on low income households in India. The datasource is the 2014
Global Findex microdata which contains individual-level survey results.
Low income households (defined as survey participants in the lower 2
within economy household income quintiles) have been chosen as the focus
group as these are the particupants which are most likely to benefit
from microfinancial services. The dependent variables are chosen based
on their correlations with household lifetime wealth.

## Summary of characteristics of respondants in the sample.

The below tables provide a summary of the respondents in the sample.
This includes a count of males and females, age groups, the income
quintiles and access to bank accounts for the respondents.

### Gender

Although the distribution of males and females in the sample is
relatively proportionate, approximately 150 more males were surveyed in
the 2014 dataset in India.

![](graphgen_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

### Education

An overwhelming majority of participants had only completely primary
education or less (forming 62% of the total sample). Only a further 31%
of applications had completed secondary education with only 1% having
completed tertiary or higher.

![](graphgen_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

### Within economy income quintile

The distrubtion of respondents is relatively even amongst the second,
third and fourth quintile. However, respondents in the poorest 20%
income bracket are significantly under represented while respondents in
the highest 20% income bracket are slightly over represented.

The 2014 sample dramatically under-represents people in the lowest 20%
household income quintile. This is a big problem because that would have
been the target demographic for microfinance, individuals with less
disposable income are more likely to be denied financial services from
the traditional sector so their underrepresentation in the Global Findex
means that the sample is skewed. I look forward to examining the sample
mix in the 2017 data to see if it’s been fixed.
![](graphgen_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

### Age of respondents

The skew of respondents is right-tailed with many more younger
participants than older ones.

![](graphgen_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

### Bank account numbers

The majority of respondents (over 55%) have a bank account.

![](graphgen_files/figure-gfm/unnamed-chunk-7-1.png)<!-- --> \#\#
Although the global findex database has a wide range of people in the
survey, the poorest 20% are under-represented in the sample

### Microfinance and income

Most microfinance institutions are targetting those in the lowest two
income quintiles who might otherwise go unserved by traditional
financial institutions.

Examining financial decisions made by respondents within the lowest 40%
income quintiles, we see the following results.

    ## [[1]]
    ##        Freq      Prop
    ## Female  484 0.4879032
    ## Male    508 0.5120968
    ## 
    ## [[2]]
    ##                            Freq      Prop
    ## completed primary or less   705 0.7106855
    ## completed tertiary or more   31 0.0312500
    ## secondary                   256 0.2580645
    ## 
    ## [[3]]
    ##                                     Freq      Prop
    ## Respondent does not have an account  513 0.5171371
    ## Respondent has an account            479 0.4828629
    ## 
    ## [[4]]
    ##       Freq        Prop
    ## 0-1      0 0.000000000
    ## 1-4      0 0.000000000
    ## 5-9      0 0.000000000
    ## 10-14    0 0.000000000
    ## 15-19  132 0.133064516
    ## 20-24  116 0.116935484
    ## 25-29  118 0.118951613
    ## 30-34  110 0.110887097
    ## 35-39  110 0.110887097
    ## 40-44  101 0.101814516
    ## 45-49   78 0.078629032
    ## 50-54   58 0.058467742
    ## 55-59   51 0.051411290
    ## 60-64   56 0.056451613
    ## 65-69   37 0.037298387
    ## 70-74   16 0.016129032
    ## 75-79    6 0.006048387
    ## 80-84    2 0.002016129
    ## 85+      1 0.001008065

### Income and education

Although across the total sample surveyed, 62% of respondents had
primary education or less, for those earning income within the lowest
40% quintiles, this is amplied suggesting that low income earners occupy
a large subset of those with primary education or less.

## Who has an account?

On the surface it seems like more people have bank accounts than not

The overall split suggests that the majority of respondents have access
to banking. ![](graphgen_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

The most common reason in 2014 stated by respondents for not having an
account is lack of money required to open up. MFIs must step in to
bridge this financial gap.
![](graphgen_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

### Income and bank account numbers

From the data, we see that examining all respondents suggests that the
majority have access to banking services. However, at a closer glance at
those in lower incomes this result is flipped. The majority of
respondents do not have a bank accout, although the split between those
who do and do not is much smaller as compared to the original sample.

![](graphgen_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

### Gender and bank account numbers

The number of survey respondents with bank accounts varies considerably
between men and women. In 2014, the majority of female respondents did
not have access to a banka ccount. However, an overwhelming majority of
males did. This gender disparity can be seen accross the developing
world and is statistically
    significant.

![](graphgen_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

    ## Warning in `[<-.factor`(`*tmp*`, list, value = "1"): invalid factor level, NA
    ## generated
    
    ## Warning in `[<-.factor`(`*tmp*`, list, value = "1"): invalid factor level, NA
    ## generated

The proportion of women who have an account:

    ## [1] 0.4693878

The proportion of men who have an account:

    ## [1] 0.6396453

Within the lowest 20%, men are more likely to have a bank account than
women: ![](graphgen_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->
Proportion of all respondents in lowest 20% income quintile with a bank
account:

    ## [1] 0.4773869

Proportion of women in lowest 20% income quintile with a bank account:

    ## [1] NaN

Proportion of men in lowest 20% income quintile with a bank account:

    ## [1] NaN

Under half of the women in low income brackets have bank accounts. Rates
of women with bank accounts in low income households are lower than the
sample average by 4pp.

\#\#Examining differences between high income respondents in India and
low income respondents. Those in the richest 20% income quintile are
over 2.7x more likely to have bank accounts than those in the poorest
20% income quintiles. This trend is exacerbated for
women.

![](graphgen_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->![](graphgen_files/figure-gfm/unnamed-chunk-20-2.png)<!-- -->

    ## [1] 2.715789

### Spending behaviour differences

Gender split analysis for highest income quintile \#\# Proportion of
women in highest 20% income quintile with bank
account

    ## [1] 0.7068493

    ## [1] 0.7994924

    ## [1] 0.7994924

# How does asset management behaviour differ amongst different people in India? Respondents show that:

## Education

The return to spending on education can vary dramatically between
countries, genders and income levels. Most studies find that the return
is statistically significant and varies between 8% and 13%. The analysis
below examines how these characters correlate with a person’s decision
to save money for education. This analysis is also extended to borrowing
behaviour as a comparator.

#### Saving for education

### Income:

Saving for education is 7pp higher ifor those in the highest 20% income
quintile than in the lowest 20% income quintile. The return to
investment in education is estimated at approximately 5-7% per anuum on
average, a rate that is considerably higher than the average bank base
rate for saving. Better financial structuring to allow low income
households to save and spend on education would help raise their
lifetime wealth function.

Proportion of low income people with an account who save for school
fees:

    ## [1] 0.2473684

Proportion of high income people with an account who save for school
fees:

    ## [1] 0.3197674

### Gender:

In the 2014 data, women with access to bank accounts were 7 percentage
points more likely to save for school fees than men, even though men
were more likely to have access to bank accounts. This pattern was seen
across all income quintiles. This really highlights that women are a
high-economic impact demographic. Although they’re underrepresented in
the financial sector, they consume financial services which correlate
with a higher average lifetime wealth. Perhaps this raises a question
about how services can be better marketed for women. In some cases,
keeping the existence of a bank account might be the big driver, in
others, it might be an education barrier.

Proportion of women with an account who save for school fees:

    ## [1] 0.3763118

Proportion of men with an account who save for school fees

    ## [1] 0.3029703

Women are 7.6 percentage points more likely to save for school fees
(human capital investment) than men.

    ## [1] 0.559

#### Borrowing for education

### Income:

When examining borrowing behaviour, the relationship is flipped. Low
income households are more likely to borrow for education than high
income households (approx 8pp more likely). This suggests that relative
to their higher income counterparts, low income households benefit more
from microfinance lending services as they have a higher propensity to
spend on education from borrowed finances.

Proportion of low income people with an account who save for school
fees:

    ## [1] 0.2052632

Proportion of high income people with an account who save for school
fees:

    ## [1] 0.127907

### Gender:

In the 2014 data, women with access to bank accounts were 5 percentage
points more likely to borrow for school fees than men, even though men
were more likely to have access to bank accounts.

Proportion of women with an account who save for school fees:

Proportion of men with an account who save for school fees:

Women are 5 percentage points more likely to borrow for school fees
(human capital investment) than men.

    ## [1] 0.559

## Paying by cash:

The 2014 data suggests that India is still a major cash economy. The
majority of respondents pay their bills and other make other
transactions by cash. This highlights that there may be a gap in the MFI
market for business-facing products. If businesses don’t have
inexpensive access to card machines and mobile payment devices, then
customers have no need to consume such products. This is a big problem
in high crime regions of India where a sizeable proportion of wealth is
lost every day to petty theft. Further analysis should aim to understand
how much might be lost due to lack of access to modern financial
technology. There is an argument here for directing funds to not just
client facing MFIs but also those that provide services for small
businesses.

# Conclusion and further considerations:

To evaluate the effect of increasing financial access for households and
microentrepreneurs, one has to look beyond the direct impact on the
household or enterprise and assess the impact on the whole economy. That
cannot be done through micro studies. In particular, even if the very
poor do not themselves gain access to financial services, they may
benefit substantially from increased employment and other opportunities
resulting from the activities of less-poor microentrepreneurs whose
access has improved. With large numbers of the nonpoor still excluded
from access to credit, these systemic effects could include trickle-down
effects for the poor from improved access for the nonpoor. However, they
could also include perverse trickle-down effects: if only a subset of
households in a village has access to credit or insurance to smooth
consumption, that subset will bid up the price of nontraded goods when a
negative shock hits the village, so excluded households will be worse
off than if nobody had access to credit or insurance (Morduch 2006).

## Better metrics for measuring financial inclusion

The fact sheet for India in the 2017 data showed that the rate of unused
banked was approximately 40% of bank accounts in the report. This means
that only 32% of users in the survey (960 of the 3000) actually have an
active bank account. This statistic suggests that just having a bank
account is not a good enough metric by itself and there are still
further challenges to go. Availability of financial markets doesn’t mean
that people make the most of the services in front of them. Further
analysis and data collection in MFI areas should aim to understand what
barriers people might face in accessing banking and other digital
financial management tools.
