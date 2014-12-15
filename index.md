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

The normal distribution is probably the most widely used statistical distribution.

It is used in statistical inference for:

1.  hypothesis testing
2.  confidence interval

--- .class #id 

## The App

This app, available at http://podgursv.shinyapps.io/project_1/, provides an interactive way to compute the Z-scode and p-value of a user-provided value given a user-specified distribution, thus providing a more convenient alternative to the traditional method of using a printed lookup table.

The app also helps the user visualize the value on the plot of the sample distribution.

--- .class #id 

## Usage

The user inputs the mean and standard deviation of the normal distribution, as well as the sample size.

Optionally, the user may change the color of the bars of the histogram, as well as switch on/off the visibility of the corresponding density curve and median value mark.

If a value is entered in the input box, the app marks it on the histogram, and computes and displays the corresponding Z-scode and p-value.

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

Based on this sample distribution, assuming the user enters `10.9` for the value, the Z-score is calculated with the well-known formula:

```r
q <- 10.9
z <- (q - mu)/sd
```

```
## [1] -0.7333333
```

And the p-value is calculated using the `pnorm` function.  Since the app computes a one-side p-value, depending on the magnitude of the user entered value compared to the mean of the sample distribution, the `lower.tail` parameter of the `pnorm` function has different values.

```r
if (q >= mu) lt <- FALSE else lt <- TRUE
p <- pnorm(q, mean = mu, sd = sd, lower.tail = lt)
```

```
## [1] 0.2316776
```
