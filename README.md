---
title: "Home Work-9"
author: "Vincent, Gins, Lilik"
date: "March 20, 2017"
output: github_document
---

---
title: "Home Work 9"
author: "Vincent, Gins, Lilik"
date: "March 23, 2017"
output: github_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Data file 
Read file "ArrestMini.csv" and save it to "ArrestMini"

```{r}
ArrestMini <- read.csv("ArrestMini.csv")
```

## "DataCleaning.R" inside the "Function" folder 
```{r}
AggregateByCase<-function(group,x){tapply(x,group,length)}
lenunique<-function(x){length(unique(x))}
UniqueAggregate<-function(group,x){tapply(x,group,lenunique)}
```

## "Plotting.R" inside "Graphs" folder
```{r}
PlotByTime<-function(time,count){ plot(count~time,
                                  xlab="Time",ylab="Counts of Council Districts Having Crime",
                                  main="The Spread of Crime",type="l",lwd=1)}
```

## "main.R" that contains the functions in both DataCleaning.R and Plotting.R
Read ArrestMini.csv and save it to ArrestMini  
```{r}
ArrestMini <- read.csv("ArrestMini.csv")
```

```{r echo=FALSE}
head(ArrestMini)
```

Ommit NA
```{r}
dat<-na.omit(ArrestMini)
```

Retrieve the "date character" from "ARRESTTIME" character string that contains date dan time
```{r}
dat$ARRESTTIME<-substr(as.character(dat$ARRESTTIME), 1, 10)
```
result (display only 20 list):
```{r echo=FALSE}
dat$ARRESTTIME [1:20]
```

Count the aggregate Council Districts on each Arrest Time day
```{r}
CrimeCount<-as.matrix(AggregateByCase(dat$ARRESTTIME,dat$COUNCIL_DISTRICT))
```
result (display 20 list):
```{r echo=FALSE}
CrimeCount [1:20, 1]
```

Count the aggregate unique Council Districts on each Arrest Time day
```{r}
CouncilCount<-as.matrix(UniqueAggregate(dat$ARRESTTIME,dat$COUNCIL_DISTRICT))
```
result:
```{r echo=FALSE}
CouncilCount
```

## A "Time-Series" Graph
Convert variable ARRESTTIME from character to date
```{r}
time<-as.Date(sort(unique(dat$ARRESTTIME)),"%Y-%m-%d")
```

Plot time and aggregate Council Districts on each Arrest Time day
```{r}
PlotByTime(time,CouncilCount[,1])
```

#Thank You....







