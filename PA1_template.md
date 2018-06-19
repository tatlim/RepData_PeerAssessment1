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



```r
activity <-
    read.csv(
        file = unzip("./activity.zip"),
        colClasses = c("integer", "Date", "integer")
    )
```


## What is mean total number of steps taken per day?

The total number of daily steps varies as shown in the plot below.



```r
daily_steps <- with(activity, tapply(steps, date, sum))

mean_daily_steps <- format(mean(daily_steps, na.rm = TRUE), scientific = FALSE)

median_daily_steps <- median(daily_steps, na.rm = TRUE)

hist(daily_steps, xlab = "Steps per Day", main = "Total Number of Steps per Day")
```

![](PA1_template_files/figure-html/daily_steps-1.png)<!-- -->

*Mean total number of daily steps* is **10766.19** and *median* **10765**.

## What is the average daily activity pattern?


```r
mean_steps_per_interval <- with(activity, tapply(steps, interval, mean, na.rm = TRUE))
max_steps_per_interval <- max(mean_steps_per_interval)
max_steps_interval <- names(which.max(mean_steps_per_interval))

plot(names(mean_steps_per_interval), mean_steps_per_interval, type = "l", xlab = "5min interval", ylab = "mean steps per interval")
```

![](PA1_template_files/figure-html/daily_activity-1.png)<!-- -->

Average daily activity peaks in the morning hours with a maximum
at **835**.

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
