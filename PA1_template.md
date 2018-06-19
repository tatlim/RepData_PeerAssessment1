---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---





## Loading and preprocessing the data

The following plots and calculations are based on [Activity Monitoring Data][1]
of an anonymous individual collected in October / November 2012.

[1]: https://d396qusza40orc.cloudfront.net/repdata/data/activity.zip





## What is mean total number of steps taken per day?

The total number of daily steps varies as shown in the plot below.


![](PA1_template_files/figure-html/daily_steps-1.png)<!-- -->

*Mean total number of daily steps* is **10766.19** and *median* **10765**.

## What is the average daily activity pattern?

![](PA1_template_files/figure-html/daily_activity-1.png)<!-- -->

*Average daily activity* peaks in the morning hours with a maximum
at interval **835**.

## Imputing missing values



Our *Activitiy Monitoring Dataset* has **2304** rows
with missing values (NA values).

My strategy for filling in these missing values will be to impute NA values
with the mean for the affected 5-minute interval.

![](PA1_template_files/figure-html/impute-1.png)<!-- -->

After imputing NA values *mean total number of daily steps* is **10766.19** and *median* **10766.19**.

## Are there differences in activity patterns between weekdays and weekends?
