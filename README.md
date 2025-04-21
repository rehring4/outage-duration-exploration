# **Shockingly Predictable:** Forecasting Outage Duration

*by Lauren May (laumay@umich.edu) and Julia Rehring (rehring@umich.edu)*

---

## Introduction

In this project, we studied power outages across the United States. We specifically focused on analyzing the **duration** of power outages and identifying the factors that led to longer outages. Our ultimate goal was to **predict outage duration** based on a variety of factors including weather, location, cause, and time of year.

---

## Data Cleaning

We preprocessed the outage data to make it more workable. Specifically:

- Created `OUTAGE.START` and `OUTAGE.RESTORATION` columns by combining the existing "date" and "time" fields.
- Dropped rows missing outage duration, as it is central to our analysis and prediction task.
- Removed outages missing start times or month values—these were important features for our analysis.
- Did **not** impute missing values due to the negligible amount of missing data.
- Removed **extreme outliers** in outage duration to better focus our model on typical patterns. Outlier removal is demonstrated below:

 <iframe
 src="assets/outlier_removal.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

After cleaning, the dataset looks like this:

|   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | OUTAGE.START        | OUTAGE.RESTORATION   |
|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:--------------------|:---------------------|
|   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |
|   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |
|   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |
|   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |
|   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |

---

## Univariate Analysis

To explore which factors might influence outage duration, we first analyzed the distributions of various features.

### Outages by Month

 <iframe
 src="assets/outages_by_month.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

There is a clear pattern: more outages occur in **summer months**, with a smaller peak in early **winter**. This suggested a possible link between seasonal weather events and outages.

### Outage Cause Distribution

 <iframe
 src="assets/outage_cause_distribution.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

As suspected, **severe weather** is the most common cause—nearly **twice as frequent** as the second most common cause, **intentional attacks**.

### Climate Anomaly (ONI) Distribution

 <iframe
 align ='center'
 src="assets/anomaly_distribution.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

The Oceanic Niño Index (ONI) helps classify climate conditions as **El Niño, La Niña, or Neutral**, based on thresholds of ±0.5°C. We explored its distribution to assess its potential relationship with outages.

### Urban Population Percentage Distribution

 <iframe
 src="assets/pct_urb_by_state.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

 This demonstrates a higher urban population in cities on the coasts and in the West. This could potentially indicate the level of infrastructure that is in place in a certain area and thus how quickly a outage could be restored.


## Bivariate Analysis

Next, we explored relationships between **outage duration** and other features.

### Outage Duration by State

 <iframe
 src="assets/duration_by_state.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

The **northeastern U.S.**—particularly **West Virginia**—tends to experience longer outages. This is consistent with the areas where urban population density was lower. This supports the hypothesis that geographic and possibly infrastructural factors play a role.

### Outage Duration by Cause

 <iframe
 src="assets/duration_by_cause.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

Surprisingly, **fuel supply emergencies** lead to the longest outages, followed by **severe weather** events.

### Average Outage Duration by Month

 <iframe
 src="assets/duration_by_month.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

The longest average outages occur in **September**. This could be linked to hurricane season or irregular fuel supply events.

### Average Outage Duration by urban Population Percentage

 <iframe
 src="assets/duration_by_pcturb.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

Interestingly, areas with a higher urban population percentage tend to have longer outages. It also seems that the **northeastern U.S.** tends to have higher a higher percentage of urban populations and longer outages.

## Interesting Aggregates

In order to further explore the data, we aggregated it in different ways to gain some insights.

### Average Outage Duration by Anomaly Level and Climate Region

 <iframe
 src="assets/pivot_anomaly_climate.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

As demonstrated by the pivot table above, longer outages tend to occur during the normal ranges of the ONI level. It also demonstrates that the Northeast region tends to have longer outages as a whole.
 
### Anomaly Levels by Month

|   MONTH |   avg_anomaly |   avg_duration |   outage_count |
|--------:|--------------:|---------------:|---------------:|
|       1 |   -0.332576   |        2590.48 |            132 |
|       2 |   -0.300763   |        2054.53 |            131 |
|       3 |   -0.120652   |        1947.72 |             92 |
|       4 |   -0.0598131  |        1493.86 |            107 |
|       5 |   -0.126271   |        1704.39 |            118 |
|       6 |   -0.072043   |        1948.4  |            186 |
|       7 |   -0.0445714  |        1680.69 |            175 |
|       8 |   -0.209272   |        2428.48 |            151 |
|       9 |   -0.213043   |        4294.52 |             92 |
|      10 |    0.0138889  |        3600.94 |            108 |
|      11 |   -0.00724638 |        1728.16 |             69 |
|      12 |    0.087037   |        3293.79 |            108 |

The above table gives insight into how the anomaly levels change during the months and how that may coorespond to longer or shorter outages.

### Outages Duration by Cause Category and Customers Affected

| CAUSE.CATEGORY                |   OUTAGE.DURATION |   CUSTOMERS.AFFECTED |
|:------------------------------|------------------:|---------------------:|
| equipment failure             |           399.13  |          2.83979e+06 |
| fuel supply emergency         |          8395.23  |          1           |
| intentional attack            |           429.98  |     356315           |
| islanding                     |           200.545 |     209749           |
| public appeal                 |          1468.45  |     159994           |
| severe weather                |          3704.41  |          1.31566e+08 |
| system operability disruption |           728.87  |          1.70555e+07 |

This table is key in demonstrating that the fact that fuel supply emergency is the cause with the longest outage duration may be an outlier, as it only affects 1 customer. Severe weather on the other hand, affects drastic numbers of customers.

## Baseline Model
To predict power outage duration, we created a baseline model using a Linear Regression pipeline. This model incorporated three key features:

`MONTH` (categorical, one-hot encoded)

`CLIMATE.REGION` (categorical, one-hot encoded)

`ANOMALY.LEVEL` (numerical, with a transformation to absolute value)

We used scikit-learn’s **Pipeline** and **ColumnTransformer** to preprocess the data and train the model. The categorical columns were encoded using OneHotEncoder, and the anomaly level was passed through a FunctionTransformer to take its absolute value. We trained the model on a train/test split and evaluated its performance using mean squared error (MSE) and mean absolute error (MAE).

### Baseline Model Performance:

| TRAINING MSE      | TESTING MSE      | TESTING MAE     |
|:------------------|-----------------:|----------------:|
| 1.49e+07          | 1.27e+07         | 2404.05         |

This simple model provided a helpful benchmark, but we suspected that additional features and more flexible transformations could yield better results.

## Final Model
For our final model, we used a more advanced approach by incorporating:

Additional categorical features: `CAUSE.CATEGORY`, `CLIMATE.CATEGORY`

A scaled numeric feature: `POPPCT_URBAN`

Polynomial expansion of `ANOMALY.LEVEL` to capture potential non-linear effects

We also introduced regularization by switching to **Ridge Regression**, which helps control overfitting.

To optimize our pipeline, we used **GridSearchCV** to tune two hyperparameters:

The degree of the polynomial features: **1–25**

The alpha parameter for Ridge Regression: **[0.1, 1.0, 10.0]**

Best parameters found via GridSearch:

Polynomial degree: 1

Ridge alpha: 0.1

This outcome suggests that linear terms provided the best generalization, but the addition of regularization and more features helped improve performance over the baseline.

### Final Model Performance:

| TRAINING MSE      | TESTING MSE      | TESTING MAE     |
|:------------------|-----------------:|----------------:|
| 1.11e+07          | 1.04e+07         | 2158.37         |

Overall, this model yielded an 18% reduction in test mean squared error compared to our baseline. The improvement suggests that capturing more information about urban population, cause type, and applying regularization led to better generalization.


