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
# sum up total daily steps
daily_steps <- with(activity, tapply(steps, date, sum))

# calculate mean daily steps
mean_daily_steps <- format(mean(daily_steps, na.rm = TRUE), scientific = FALSE)

# find median of daily steps
median_daily_steps <- median(daily_steps, na.rm = TRUE)

# plot histogram of daily steps
hist(daily_steps,
     xlab = "Steps per Day",
     main = "Total Number of Steps per Day")
```

![](PA1_template_files/figure-html/daily_steps-1.png)<!-- -->

*Mean total number of daily steps* is **10766.19** and *median* **10765**.

## What is the average daily activity pattern?


```r
# calculate mean steps for each 5min interval
mean_steps_per_interval <- with(activity, tapply(steps, interval, mean, na.rm = TRUE))

# find maximum steps done in a 5min interval
max_steps_per_interval <- max(mean_steps_per_interval)

# identify the 5min interval with maximum steps
max_steps_interval <- names(which.max(mean_steps_per_interval))

# plot average steps per 5min interval
plot(
    names(mean_steps_per_interval),
    mean_steps_per_interval,
    type = "l",
    xlab = "5min interval",
    ylab = "mean steps per interval"
)
```

![](PA1_template_files/figure-html/daily_activity-1.png)<!-- -->

*Average daily activity* peaks in the morning hours with a maximum
at interval **835**.

## Imputing missing values


```r
# logical vector of missing steps
missing_steps <- is.na(activity$steps)

# number of rows with NA steps
count_missing_steps <- sum(missing_steps)
```

Our *Activitiy Monitoring Dataset* has **2304** rows
with missing values (NA values).

My strategy for filling in these missing values will be to impute NA values
with the mean for the affected 5-minute interval.


```r
# create a copy of the original data frame
imputed_activity <- data.frame(activity)

# replace NAs with mean steps for affected interval
imputed_activity[missing_steps, ]$steps <- 
    mean_steps_per_interval[as.character(imputed_activity[missing_steps, ]$interval)]

# sum up total daily steps
imp_daily_steps <- with(imputed_activity, tapply(steps, date, sum))

# calculate mean daily steps
mean_imp_daily_steps <-
    format(mean(imp_daily_steps, na.rm = TRUE), scientific = FALSE)

# find median of daily steps
median_imp_daily_steps <-
    format(median(imp_daily_steps, na.rm = TRUE), scientific = FALSE)

# plot histogram of daily steps
hist(imp_daily_steps,
     xlab = "Steps per Day",
     main = "Total Number of Steps per Day (NAs imputed)")
```

![](PA1_template_files/figure-html/impute-1.png)<!-- -->

After imputing NA values *mean total number of daily steps* is **10766.19** and *median* **10766.19**.

## Are there differences in activity patterns between weekdays and weekends?
