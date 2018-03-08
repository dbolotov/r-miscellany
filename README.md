
-   [R-miscellany](#r-miscellany)
-   [Data reading and writing](#data-reading-and-writing)
-   [Data manipulation](#data-manipulation)
-   [Time series data](#time-series-data)
-   [Plots](#plots)
-   [Rmarkdown templates](#rmarkdown-templates)
-   [Extra misc](#extra-misc)

<!-- README.md is generated from README.Rmd. Please edit that file -->
### R-miscellany

A collection of useful R code bits I'm tired of looking up.

### Data reading and writing

### Data manipulation

Drop columns from data frame by name:

``` r
iris[!colnames(iris) %in% c("Sepal.Length","Sepal.Width")]
```

Add `NA` padding to end of a vector:

``` r
a <- c(1,2,3)
length(a) <- 5 #add 2 NA elements
```

### Time series data

#### Linear interpolation for irregular intervals

``` r
library(zoo)

# dataset with irregular time intervals
t_irr <- as.POSIXct(c('2017-01-01T00:00:00S','2017-01-01T00:02:01S','2017-01-01T00:07:32S',
                      '2017-01-01T00:10:00S'), format = '%Y-%m-%dT%H:%M:%SS')
vals <- c(0,5,9,10)
df1 <- data.frame(t_irr,vals)

# time sequence with regular intervals
t_seq <- zoo(order.by=(as.POSIXct(seq(min(df1$t_irr), max(df1$t_irr), by = '1 min'))))

# merge irregular time series with t_seq
t_merged <- zoo::merge.zoo(zoo(x=df1[,c('vals')], order.by = df1$t_irr), t_seq)

# linear interpolation
t_interpolated <- zoo::na.approx(t_merged)

# discard rows where timestamp is not from t_seq
t_interpolated_2 <- t_interpolated[index(t_interpolated) %in% index(t_seq)]

# convert zoo object to data frame
t_interpolated_3 <- zoo::fortify.zoo(t_interpolated_2)
```

### Plots

Four plots in one graph:

``` r
par(mfrow=c(2,2))
```

Two series (same scale) in one graph:

Two series (different scales) in one graph:

### Rmarkdown templates

``` text
# ---
# title: "Document Title"
# output: 
#   html_document:
#     theme: cerulean
#     highlight: textmate
#     fig_width: 8
#     fig_height: 5
#     toc: true
# ---
# 
# ```{r setup, include=FALSE}
# knitr::opts_chunk$set(echo = TRUE)
# knitr::opts_knit$set(root.dir = "some/directory")
# ```
```

### Extra misc

Set language to English:

``` r
Sys.setenv(LANG='en')
```
