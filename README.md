# **Shockingly Predictable:** Forecasting Outage Duration with Climate & Calendar Clues

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
 src="assets/outages_cause_distribution.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

As suspected, **severe weather** is the most common cause—nearly **twice as frequent** as the second most common cause, **intentional attacks**.

### Climate Anomaly (ONI) Distribution

 <iframe
 src="assets/anomaly_distribution.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

The Oceanic Niño Index (ONI) helps classify climate conditions as **El Niño, La Niña, or Neutral**, based on thresholds of ±0.5°C. We explored its distribution to assess its potential relationship with outages.

---

## Bivariate Analysis

Next, we explored relationships between **outage duration** and other features.

### Outage Duration by State

 <iframe
 src="assets/duration_by_state.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

The **northeastern U.S.**—particularly **West Virginia**—tends to experience longer outages. This supports the hypothesis that geographic and possibly infrastructural factors play a role.

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

---
