Home Work 9
================
Vincent, Gins, Lilik
March 23, 2017

Data file
---------

``` r
ArrestMini <- read.csv("ArrestMini.csv")
```

Create "DataCleaning.R" inside "Function" folder
------------------------------------------------

``` r
AggregateByCase<-function(group,x){tapply(x,group,length)}
lenunique<-function(x){length(unique(x))}
UniqueAggregate<-function(group,x){tapply(x,group,lenunique)}
```

Create "Plotting.R" inside "Graphs" folder
------------------------------------------

``` r
PlotByTime<-function(time,count){ plot(count~time,
                                  xlab="Time",ylab="Counts of Council Districts Having Crime",
                                  main="The Spread of Crime",type="l",lwd=1)}
```

Create "main.R" using the functions in both DataCleaning.R and Plotting.R
-------------------------------------------------------------------------

Read ArrestMini.csv and save it to ArrestMini

``` r
ArrestMini <- read.csv("ArrestMini.csv")
```

    ##            ARRESTTIME COUNCIL_DISTRICT
    ## 1 2016-09-12T22:53:00                1
    ## 2 2016-12-26T20:36:00                7
    ## 3 2016-12-27T15:19:00                4
    ## 4 2017-01-04T20:09:00                1
    ## 5 2017-01-07T22:28:00                6
    ## 6 2016-09-18T13:55:00                6

Ommit NA

``` r
dat<-na.omit(ArrestMini)
```

Retrieve the "date character" from "ARRESTTIME" character string that contains date dan time

``` r
dat$ARRESTTIME<-substr(as.character(dat$ARRESTTIME), 1, 10)
```

result:

    ##  [1] "2016-09-12" "2016-12-26" "2016-12-27" "2017-01-04" "2017-01-07"
    ##  [6] "2016-09-18" "2016-09-19" "2016-09-19" "2016-11-08" "2016-10-08"

List Council Districts based on each ARRESTTIME

``` r
CrimeCount<-as.matrix(AggregateByCase(dat$ARRESTTIME,dat$COUNCIL_DISTRICT))
```

result (display 10 list):

    ##  [1] 3 1 2 1 1 1 1 1 1 2

Count the aggregate Council Districts on each Arrest Time day

``` r
CouncilCount<-as.matrix(UniqueAggregate(dat$ARRESTTIME,dat$COUNCIL_DISTRICT))
```

result (display only 10):

    ## 2014-11-16 2015-05-29 2015-11-04 2016-02-12 2016-02-17 2016-03-03 
    ##          1          1          1          1          1          1 
    ## 2016-04-04 2016-04-08 2016-04-10 2016-04-12 
    ##          1          1          1          1

Plotting
--------

Convert variable ARRESTTIME from character to date

``` r
time<-as.Date(sort(unique(dat$ARRESTTIME)),"%Y-%m-%d")
```

Plot time and aggregate Council Districts on each Arrest Time day

``` r
PlotByTime(time,CouncilCount[,1])
```

![](README_files/figure-markdown_github/unnamed-chunk-14-1.png)
