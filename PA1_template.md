# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

```r
dataset<-read.csv("activity.csv")
```

## What is mean total number of steps taken per day?
##1. Total number of steps taken per day

```r
stepsperday<-tapply(dataset$steps,dataset$date,sum)
```

##2. Histogram of the total number of steps taken each day

```r
barplot(stepsperday)
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png) 

##3. Mean and median of the total number of steps taken per day

##Mean

```r
mean(stepsperday, na.rm = TRUE)
```

```
## [1] 10766.19
```
##Mean

```r
median(stepsperday, na.rm = TRUE)
```

```
## [1] 10765
```



## What is the average daily activity pattern?

##1. Time series plot of average daily activity pattern

```r
average_activity_pattern<-tapply(dataset$steps,dataset$interval,mean, na.rm=TRUE)
x<-dimnames(average_activity_pattern)[[1]]
y<- average_activity_pattern
plot(x,y,"l")
```

![](PA1_template_files/figure-html/unnamed-chunk-6-1.png) 

##2. 5-minute interval which has the maximum average number of steps

```r
which.max(average_activity_pattern)
```

```
## 835 
## 104
```


## Inputing missing values
##1.Total number of missing values in the dataset

```r
sum(is.na(dataset$steps))
```

```
## [1] 2304
```


##2. Create a new dataset that is equal to the original dataset but with the missing data filled in with the mean for that 5-minute interval

```r
for (i in 1:nrow(dataset)){
    if (is.na(dataset$steps[i])){
    dataset$steps[i]<-average_activity_pattern[rownames(average_activity_pattern)==dataset$interval[i]]
  }
}
```

##3 Histogram of the total number of steps taken each day

```r
stepsperday<-tapply(dataset$steps,dataset$date,sum)
barplot(stepsperday)
```

![](PA1_template_files/figure-html/unnamed-chunk-10-1.png) 

##Mean and median of the total number of steps taken per day

##Mean

```r
mean(stepsperday, na.rm = TRUE)
```

```
## [1] 10766.19
```
##Mean

```r
median(stepsperday, na.rm = TRUE)
```

```
## [1] 10766.19
```

There is no significant difference for mean and median number of daily steps between the two methods 

## Are there differences in activity patterns between weekdays and weekends?

