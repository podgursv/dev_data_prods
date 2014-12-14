---
title       : Shiny App for Normal Distributions
subtitle    : Project for the Coursera course "Developing Data Products"
author      : Vlad Podgurschi
job         : Coursera Student
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction

The normal distribution is the most used probability distribution in statistics.

It is used in statistical inference for:

1.  hypothesis testing:  given an test value, get the probability that the value may appear by chance in observation.
2.  confidence interval:  determine what range of values a value may take so that we are confident in a specified degree  XXXX

--- .class #id 

## The App

The app [http://podgursv.shinyapps.io/project_1] helps determining in an interactive way the Z-scode and p-value of a user-provided quantile given a user-specified distribution.  This is convenient, because traditionally, a printed lookup table was used.

The app also helps the user visualize the value in the context of the sample distribution.

--- .class #id 

## Usage

The user inputs the desired sample size, the and the mean and standard deviation of the distribution.  The larger the sample size, the better the more simetric and XXX the distribution appears.

Optionally, the user may change the color of the histogram bars, as well as turn on/off the visibility of the corresponding density curve and median.

If an quantile is entered in the input box, the app marks it on the histogram, and computes the corresponding Z-scode and p-value.

--- .class #id 

## Internals

The distribution is generated using the `rnorm` function.  For example, assuming the user ask for a sample of size `300`, having the mean `12`, and standard deviation `1.5`, the distribution is generated using the following function call:

```r
n <- 300
mu <- 12
sd <- 1.5
data <- rnorm(n, mean = mu, sd = sd)
```

--- .class #id 

Based on this sample distribution, assuming the user enters the value `10.9` for the quantile, the Z-score is calculated with the well-known formula:

```r
q <- 10.9
z <- (q - mu)/sd
```

```
## [1] -7.133333
```

And the p-value is calculated using the `pnorm` function.  Since the app computes a one-side p-value, depending on the quantile magnitude compared to the sample distribution mean, the `lower.tail` parameter of the `pnorm` function has different values.

```r
if (q >= mu) lt <- FALSE else lt <- TRUE
p <- pnorm(q, mean = mu, sd = sd, lower.tail = lt)
```

```
## [1] 4.898346e-13
```





