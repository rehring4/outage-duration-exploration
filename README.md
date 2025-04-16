# **Shockingly Predictable:** Forecasting Outage Duration with Climate & Calendar Clues

by Lauren May (laumay@umich.edu) and Julia Rehring (rehring@umich.edu)

---

## Introduction

In this project, we studied power outages across the United States. We specifically were interested in anlyzing the duration of power outages and determining the factors that led to longer outages. With this we also had the goal of predicting how long an outage would be based on various factors including weather, location, cause and more.

## Data Cleaning

We preprecessed the outage data in order to work with it more efficiently. First, we chose to create respective outage start and outage restoration columns by combining the existing "date" and "time" columns. We also chose to drop any rows in the dataframe that did not contain a value for the outage duration, as that is the main focus of our anlaysis and prediction. With this, we also dropped any outags that did not contain a start time or a month as we found that to be important to our analysis. We chose not to impute this data as the number of rows with missing values was negligible. Finally, we chose to remove any outages with an extreme outage duration, as the goal of our analysis and predictive model was to give a more specific concentrated prediction of outage duration. The outlier removal is demonstrated by the graph below:
 <iframe
 src="assets/outlier_removal.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

After cleaning the data this is the final dataframe:
|   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | OUTAGE.START        | OUTAGE.RESTORATION   |
|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:--------------------|:---------------------|
|   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |
|   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |
|   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |
|   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |
|   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |

## Univariate Analysis
In order to explore our question of what factors affect the duration of a power outage we chose to look at the distribution of some of the features in the data. First we explored how many outages occured in each month:
 <iframe
 src="assets/outages_by_month.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>
 There is an interesting pattern of more outages occuring in the summer months, as well as an uptick in the early months of winter. This indicated to us that more outages may be due to changes in the weather. To verify this, we explored the distribution of the causes of outages:
 <iframe
 src="assets/outages_cause_distribution.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>
 As we suspected, most outages were caused by severe weather. This cause is almost double the second amount, being intentional attacks. To further explore how weather might be affecting the outages, we chose to explore the Anomaly Level. As detailed in the notes on this dataset, this number is the Oceanic Niño Index (ONI), which is a measure used to indicate El Niño and La Niña events. The measurement has threshold of +/- 0.5oC that defines if the climate was warm, normal or cold. The distribution of anomaly levels is displayed below:
 <iframe
 src="assets/anomaly_distribution.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>



## Assessment of Missingness

Here's what a Markdown table looks like. Note that the code for this table was generated _automatically_ from a DataFrame, using

```py
print(counts[['Quarter', 'Count']].head().to_markdown(index=False))
```

| Quarter     |   Count |
|:------------|--------:|
| Fall 2020   |       3 |
| Winter 2021 |       2 |
| Spring 2021 |       6 |
| Summer 2021 |       4 |
| Fall 2021   |      55 |

---

## Hypothesis Testing


---
