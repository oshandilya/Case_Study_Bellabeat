Case Study
================
Ojas

## Installing and loading common packages and libraries

we will load all the necessary libraries required to process, analyze,
and visualize the data.

``` r
install.packages('tidyverse')
```

    ## Installing package into 'C:/Users/oshan/Documents/R/win-library/4.1'
    ## (as 'lib' is unspecified)

    ## package 'tidyverse' successfully unpacked and MD5 sums checked
    ## 
    ## The downloaded binary packages are in
    ##  C:\Users\oshan\AppData\Local\Temp\RtmpEnuwT0\downloaded_packages

``` r
install.packages('dplyr')
```

    ## Installing package into 'C:/Users/oshan/Documents/R/win-library/4.1'
    ## (as 'lib' is unspecified)

    ## package 'dplyr' successfully unpacked and MD5 sums checked
    ## 
    ## The downloaded binary packages are in
    ##  C:\Users\oshan\AppData\Local\Temp\RtmpEnuwT0\downloaded_packages

``` r
install.packages('janitor')
```

    ## Installing package into 'C:/Users/oshan/Documents/R/win-library/4.1'
    ## (as 'lib' is unspecified)

    ## package 'janitor' successfully unpacked and MD5 sums checked
    ## 
    ## The downloaded binary packages are in
    ##  C:\Users\oshan\AppData\Local\Temp\RtmpEnuwT0\downloaded_packages

``` r
install.packages('skimr')
```

    ## Installing package into 'C:/Users/oshan/Documents/R/win-library/4.1'
    ## (as 'lib' is unspecified)

    ## package 'skimr' successfully unpacked and MD5 sums checked
    ## 
    ## The downloaded binary packages are in
    ##  C:\Users\oshan\AppData\Local\Temp\RtmpEnuwT0\downloaded_packages

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(janitor)
```

    ## 
    ## Attaching package: 'janitor'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     chisq.test, fisher.test

``` r
library(skimr)
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.6     v stringr 1.4.0
    ## v tidyr   1.2.0     v forcats 0.5.1
    ## v readr   2.1.2

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

## Loading CSV files

We will use *dailyActivity_merged.csv*, *sleepDay_merged.csv*, and
*dailySteps_merged.csv* datasets in this analysis.

``` r
daily_activity <- read.csv("dailyActivity_merged.csv")
sleep_day <- read.csv("sleepDay_merged.csv")
daily_steps <- read.csv("dailySteps_merged.csv")
```

## Exploring a few key tables

We will now look into our datasets *daily_activity*

``` r
head(daily_activity)
```

    ##           Id ActivityDate TotalSteps TotalDistance TrackerDistance
    ## 1 1503960366    4/12/2016      13162          8.50            8.50
    ## 2 1503960366    4/13/2016      10735          6.97            6.97
    ## 3 1503960366    4/14/2016      10460          6.74            6.74
    ## 4 1503960366    4/15/2016       9762          6.28            6.28
    ## 5 1503960366    4/16/2016      12669          8.16            8.16
    ## 6 1503960366    4/17/2016       9705          6.48            6.48
    ##   LoggedActivitiesDistance VeryActiveDistance ModeratelyActiveDistance
    ## 1                        0               1.88                     0.55
    ## 2                        0               1.57                     0.69
    ## 3                        0               2.44                     0.40
    ## 4                        0               2.14                     1.26
    ## 5                        0               2.71                     0.41
    ## 6                        0               3.19                     0.78
    ##   LightActiveDistance SedentaryActiveDistance VeryActiveMinutes
    ## 1                6.06                       0                25
    ## 2                4.71                       0                21
    ## 3                3.91                       0                30
    ## 4                2.83                       0                29
    ## 5                5.04                       0                36
    ## 6                2.51                       0                38
    ##   FairlyActiveMinutes LightlyActiveMinutes SedentaryMinutes Calories
    ## 1                  13                  328              728     1985
    ## 2                  19                  217              776     1797
    ## 3                  11                  181             1218     1776
    ## 4                  34                  209              726     1745
    ## 5                  10                  221              773     1863
    ## 6                  20                  164              539     1728

``` r
glimpse(daily_activity)
```

    ## Rows: 940
    ## Columns: 15
    ## $ Id                       <dbl> 1503960366, 1503960366, 1503960366, 150396036~
    ## $ ActivityDate             <chr> "4/12/2016", "4/13/2016", "4/14/2016", "4/15/~
    ## $ TotalSteps               <int> 13162, 10735, 10460, 9762, 12669, 9705, 13019~
    ## $ TotalDistance            <dbl> 8.50, 6.97, 6.74, 6.28, 8.16, 6.48, 8.59, 9.8~
    ## $ TrackerDistance          <dbl> 8.50, 6.97, 6.74, 6.28, 8.16, 6.48, 8.59, 9.8~
    ## $ LoggedActivitiesDistance <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ~
    ## $ VeryActiveDistance       <dbl> 1.88, 1.57, 2.44, 2.14, 2.71, 3.19, 3.25, 3.5~
    ## $ ModeratelyActiveDistance <dbl> 0.55, 0.69, 0.40, 1.26, 0.41, 0.78, 0.64, 1.3~
    ## $ LightActiveDistance      <dbl> 6.06, 4.71, 3.91, 2.83, 5.04, 2.51, 4.71, 5.0~
    ## $ SedentaryActiveDistance  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ~
    ## $ VeryActiveMinutes        <int> 25, 21, 30, 29, 36, 38, 42, 50, 28, 19, 66, 4~
    ## $ FairlyActiveMinutes      <int> 13, 19, 11, 34, 10, 20, 16, 31, 12, 8, 27, 21~
    ## $ LightlyActiveMinutes     <int> 328, 217, 181, 209, 221, 164, 233, 264, 205, ~
    ## $ SedentaryMinutes         <int> 728, 776, 1218, 726, 773, 539, 1149, 775, 818~
    ## $ Calories                 <int> 1985, 1797, 1776, 1745, 1863, 1728, 1921, 203~

``` r
colnames(daily_activity)
```

    ##  [1] "Id"                       "ActivityDate"            
    ##  [3] "TotalSteps"               "TotalDistance"           
    ##  [5] "TrackerDistance"          "LoggedActivitiesDistance"
    ##  [7] "VeryActiveDistance"       "ModeratelyActiveDistance"
    ##  [9] "LightActiveDistance"      "SedentaryActiveDistance" 
    ## [11] "VeryActiveMinutes"        "FairlyActiveMinutes"     
    ## [13] "LightlyActiveMinutes"     "SedentaryMinutes"        
    ## [15] "Calories"

*sleep_day*

``` r
head(sleep_day)
```

    ##           Id              SleepDay TotalSleepRecords TotalMinutesAsleep
    ## 1 1503960366 4/12/2016 12:00:00 AM                 1                327
    ## 2 1503960366 4/13/2016 12:00:00 AM                 2                384
    ## 3 1503960366 4/15/2016 12:00:00 AM                 1                412
    ## 4 1503960366 4/16/2016 12:00:00 AM                 2                340
    ## 5 1503960366 4/17/2016 12:00:00 AM                 1                700
    ## 6 1503960366 4/19/2016 12:00:00 AM                 1                304
    ##   TotalTimeInBed
    ## 1            346
    ## 2            407
    ## 3            442
    ## 4            367
    ## 5            712
    ## 6            320

``` r
glimpse(sleep_day)
```

    ## Rows: 413
    ## Columns: 5
    ## $ Id                 <dbl> 1503960366, 1503960366, 1503960366, 1503960366, 150~
    ## $ SleepDay           <chr> "4/12/2016 12:00:00 AM", "4/13/2016 12:00:00 AM", "~
    ## $ TotalSleepRecords  <int> 1, 2, 1, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, ~
    ## $ TotalMinutesAsleep <int> 327, 384, 412, 340, 700, 304, 360, 325, 361, 430, 2~
    ## $ TotalTimeInBed     <int> 346, 407, 442, 367, 712, 320, 377, 364, 384, 449, 3~

``` r
colnames(sleep_day)
```

    ## [1] "Id"                 "SleepDay"           "TotalSleepRecords" 
    ## [4] "TotalMinutesAsleep" "TotalTimeInBed"

*daily_steps*

``` r
head(daily_steps)
```

    ##           Id ActivityDay StepTotal
    ## 1 1503960366   4/12/2016     13162
    ## 2 1503960366   4/13/2016     10735
    ## 3 1503960366   4/14/2016     10460
    ## 4 1503960366   4/15/2016      9762
    ## 5 1503960366   4/16/2016     12669
    ## 6 1503960366   4/17/2016      9705

``` r
glimpse(daily_steps)
```

    ## Rows: 940
    ## Columns: 3
    ## $ Id          <dbl> 1503960366, 1503960366, 1503960366, 1503960366, 1503960366~
    ## $ ActivityDay <chr> "4/12/2016", "4/13/2016", "4/14/2016", "4/15/2016", "4/16/~
    ## $ StepTotal   <int> 13162, 10735, 10460, 9762, 12669, 9705, 13019, 15506, 1054~

``` r
colnames(daily_steps)
```

    ## [1] "Id"          "ActivityDay" "StepTotal"

Note that all datasets have the ‘Id’ field - this can be used to merge
the datasets.

If you look into the daily_activity dataset you will see data of
daily_steps is already present in daily_activity$TotalSteps. This is the
reason why other datasets were not loaded.

## Understanding some summary statistics

We will use *n_distinct()* and *nrow* to count unique values and number
of rows respectively. As Id is the only column that can used to identify
different users, we will use it to calculate number of unique users.

``` r
n_distinct(daily_activity$Id)
```

    ## [1] 33

``` r
n_distinct(sleep_day$Id)
```

    ## [1] 24

This shows that *daily)activity* contains information of 33 users
whereas *sleep_day* contains 24 unique users. As for the number of
observations in each datasets

``` r
nrow(daily_activity)
```

    ## [1] 940

``` r
nrow(sleep_day)
```

    ## [1] 413

*summary()* is used to to summarize and give your key insights from the
data.

Here in the *daily_activity* dataset:

``` r
daily_activity %>%  
  select(TotalSteps,
         TotalDistance,
         SedentaryMinutes,VeryActiveMinutes,Calories) %>%
  summary()
```

    ##    TotalSteps    TotalDistance    SedentaryMinutes VeryActiveMinutes
    ##  Min.   :    0   Min.   : 0.000   Min.   :   0.0   Min.   :  0.00   
    ##  1st Qu.: 3790   1st Qu.: 2.620   1st Qu.: 729.8   1st Qu.:  0.00   
    ##  Median : 7406   Median : 5.245   Median :1057.5   Median :  4.00   
    ##  Mean   : 7638   Mean   : 5.490   Mean   : 991.2   Mean   : 21.16   
    ##  3rd Qu.:10727   3rd Qu.: 7.713   3rd Qu.:1229.5   3rd Qu.: 32.00   
    ##  Max.   :36019   Max.   :28.030   Max.   :1440.0   Max.   :210.00   
    ##     Calories   
    ##  Min.   :   0  
    ##  1st Qu.:1828  
    ##  Median :2134  
    ##  Mean   :2304  
    ##  3rd Qu.:2793  
    ##  Max.   :4900

The summary of *daily_activity* shows that the average steps taken in a
day by a user is 7406, which is more than the minimum recommended steps
per day but less than recommended steps per day for health by CDC.
Looking the SedentaryMinutes we get to know that an average person is
sitting idle and not doing any physical activity for about 16.52
hours(991.2 minutes), which is very high. On average CDC recommends a
person to do vigorous activity for atleast 75 minutes a week, from the
dataset we can see that on average 21.16 minutes is the time spent to do
vigorous activity which acounts to 148.12 minutes. So we can say on
average a fitbit user is doing more activity than recommended and
availing more health benefits. Furthermore, on average a fitbit user is
burning 2304 calories per day which depends is good or not on your goal.
To lose weight on average 3500 calories needs to be burned according to
CDC. On average a person burns 1800 calories a day, in that sense a
fitbit user is doing better.

For the *sleep_day* dataset:

``` r
sleep_day %>%  
  select(TotalSleepRecords,
  TotalMinutesAsleep,
  TotalTimeInBed) %>%
  summary()
```

    ##  TotalSleepRecords TotalMinutesAsleep TotalTimeInBed 
    ##  Min.   :1.000     Min.   : 58.0      Min.   : 61.0  
    ##  1st Qu.:1.000     1st Qu.:361.0      1st Qu.:403.0  
    ##  Median :1.000     Median :433.0      Median :463.0  
    ##  Mean   :1.119     Mean   :419.5      Mean   :458.6  
    ##  3rd Qu.:1.000     3rd Qu.:490.0      3rd Qu.:526.0  
    ##  Max.   :3.000     Max.   :796.0      Max.   :961.0

The summary of *sleep_day* shows that on an average a fitbit user is
sleeping for 419.5 minutes(6.99 hours) which is just touches the
recommended sleep of 7 hours in a day. If you look at the time spent on
bed, average time comes out to be 458.6 which means that a person is
spending 39.1 minutes laying on bed. According to Health Central, people
should not spend more than 1 hour in bed awake.

## Merging these two datasets together

We will use Inner Join to combine these two datasets to gain more
insight on the relation between daily activity and sleep cycle of these
fibit users

``` r
combined_data <- merge(sleep_day, daily_activity, by="Id")
```

Take a look at how many participants are in this data set.

``` r
n_distinct(combined_data$Id)
```

    ## [1] 24

As we used Inner join, the users whose sleep cycle information were not
recorded are excluded from the combined dataset. We can use Outer Join
if we want to include those data in the combined dataset.

``` r
glimpse(combined_data)
```

    ## Rows: 12,441
    ## Columns: 19
    ## $ Id                       <dbl> 1503960366, 1503960366, 1503960366, 150396036~
    ## $ SleepDay                 <chr> "4/12/2016 12:00:00 AM", "4/12/2016 12:00:00 ~
    ## $ TotalSleepRecords        <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, ~
    ## $ TotalMinutesAsleep       <int> 327, 327, 327, 327, 327, 327, 327, 327, 327, ~
    ## $ TotalTimeInBed           <int> 346, 346, 346, 346, 346, 346, 346, 346, 346, ~
    ## $ ActivityDate             <chr> "5/7/2016", "5/6/2016", "5/1/2016", "4/30/201~
    ## $ TotalSteps               <int> 11992, 12159, 10602, 14673, 13162, 10735, 153~
    ## $ TotalDistance            <dbl> 7.71, 8.03, 6.81, 9.25, 8.50, 6.97, 9.80, 8.9~
    ## $ TrackerDistance          <dbl> 7.71, 8.03, 6.81, 9.25, 8.50, 6.97, 9.80, 8.9~
    ## $ LoggedActivitiesDistance <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ~
    ## $ VeryActiveDistance       <dbl> 2.46, 1.97, 2.29, 3.56, 1.88, 1.57, 5.29, 2.9~
    ## $ ModeratelyActiveDistance <dbl> 2.12, 0.25, 1.60, 1.42, 0.55, 0.69, 0.57, 1.0~
    ## $ LightActiveDistance      <dbl> 3.13, 5.81, 2.92, 4.27, 6.06, 4.71, 3.94, 4.8~
    ## $ SedentaryActiveDistance  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ~
    ## $ VeryActiveMinutes        <int> 37, 24, 33, 52, 25, 21, 73, 45, 48, 16, 31, 7~
    ## $ FairlyActiveMinutes      <int> 46, 6, 35, 34, 13, 19, 14, 24, 28, 12, 23, 11~
    ## $ LightlyActiveMinutes     <int> 175, 289, 246, 217, 328, 217, 216, 250, 189, ~
    ## $ SedentaryMinutes         <int> 833, 754, 730, 712, 728, 776, 814, 857, 782, ~
    ## $ Calories                 <int> 1821, 1896, 1820, 1947, 1985, 1797, 2013, 195~

``` r
combined_data %>% 
  select(TotalSteps,SedentaryMinutes,VeryActiveMinutes,TotalMinutesAsleep,Calories) %>% 
  summary()
```

    ##    TotalSteps    SedentaryMinutes VeryActiveMinutes TotalMinutesAsleep
    ##  Min.   :    0   Min.   :   0.0   Min.   :  0.00    Min.   : 58.0     
    ##  1st Qu.: 4660   1st Qu.: 659.0   1st Qu.:  0.00    1st Qu.:361.0     
    ##  Median : 8596   Median : 734.0   Median :  8.00    Median :432.0     
    ##  Mean   : 8117   Mean   : 799.2   Mean   : 23.97    Mean   :419.4     
    ##  3rd Qu.:11317   3rd Qu.: 853.0   3rd Qu.: 36.00    3rd Qu.:492.0     
    ##  Max.   :22988   Max.   :1440.0   Max.   :210.00    Max.   :796.0     
    ##     Calories   
    ##  Min.   :   0  
    ##  1st Qu.:1783  
    ##  Median :2162  
    ##  Mean   :2329  
    ##  3rd Qu.:2865  
    ##  Max.   :4900

Looking at *combined_data* we get to know that on average more the
active minutes spent by an user more is their minutes asleep. That is
the more you burn calories better gets your sleep cycle.

## Visualizing to gain insights

We will use *ggplot()* from ggplot2 to visualize our data and look into
the pattern and trends in the dataset.

``` r
ggplot(data=daily_activity, aes(x=TotalSteps, y=Calories)) + geom_point() +
  stat_smooth(method = lm) + 
  labs(title = "Relation between Total Steps and Calories burnt in a day")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](Case_Study_Bellabeat_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->
As we can see there is a positive relation between Total steps and
Calories burnt, which tells us that more steps taken by a fitbit user,
more calories were burnt by them.

``` r
ggplot(data=daily_activity, aes(x=VeryActiveMinutes,y=Calories)) + geom_point() +
  stat_smooth(method = lm) + 
  labs(title = "Relation between Very Active Minutes and Calories burnt")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](Case_Study_Bellabeat_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->
The relation between Active minutes and Calories burn tis positive
meaning more a person spends doing activity more calories will be burnt
by that person.

``` r
ggplot(data = daily_activity, aes(x=SedentaryMinutes,y=Calories)) + geom_point() +
  stat_smooth(method = lm) + 
  labs(title = "Relation between Sedentary Minutes and Calories burnt")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](Case_Study_Bellabeat_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->
The relation between Sedentary minutes and Calories burnt comes to be
almost linear inclined toward negetive side. This means that if a user
is idle the calories burnt will not be affected much but as the idle
time increase the calories burnt will be less than that of a person who
is not idle for that amount of time.

``` r
ggplot(data =sleep_day, aes(x=TotalMinutesAsleep,y=TotalTimeInBed)) + geom_point() +
  stat_smooth(method = lm) + 
  labs(title = "Relation between Total minutes asleep and Total time in bed")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](Case_Study_Bellabeat_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->
This visualization tells uss the relation etween Total time asleep and
Total time in bed. As most of the points are near the line, it tells us
that most of the time time spent on bed is similar to time asleep.
