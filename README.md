
-   [R-miscellany](#r-miscellany)
-   [Data reading and writing](#data-reading-and-writing)
-   [Data manipulation](#data-manipulation)
-   [Time series data](#time-series-data)
-   [Plots](#plots)
-   [Rmarkdown](#rmarkdown)
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

Two series in one graph (same scale):

``` r
plot(ts_dat$time, ts_dat$f1, col = 'blue', type = 'o', cex = 0.3,
     xlab = 'time', ylab = 'f1', cex.lab = 0.8, cex.axis = 0.7)
points(ts_dat$time, ts_dat$f2, col = 'black', type = 'o', cex = 0.3,
     title('Plot Title',cex.main = 0.9))
```

Two series in one graph (different scales):

``` r
plot(ts_dat$time, ts_dat$f1, col = 'blue', pch = 20, cex = 0.3,
     xlab = 'time', ylab = 'f1', cex.lab = 0.8, cex.axis = 0.7)
par(new=TRUE)
plot(ts_dat$time, ts_dat$f2, col = 'red', pch = 19, cex = 0.3,
     yaxt = 'n', ylab = NA, xlab = NA, lwd = 1, title('Plot Title',
     cex.main = 0.9), cex.lab = 0.7, cex.axis = 0.7)
axis(4, cex.axis = 0.7)
mtext("right y axis", side=4, cex = 0.8)
```

### Rmarkdown

#### template

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

#### `theme`

Themes: "default", "cerulean", "journal", "flatly", "readable", "spacelab", "united", "cosmo", "lumen", "paper", "sandstone", "simplex", "yeti". Pass null for no theme (in this case you can use the css parameter to add your own styles).

#### `highlight`

Styles: "default", "tango", "pygments", "kate", "monochrome", "espresso", "zenburn", "haddock", "textmate". Pass null to prevent syntax highlighting.

[More info](https://rmarkdown.rstudio.com/html_document_format.html)

### Extra misc

Set language to English:

``` r
Sys.setenv(LANG='en')
```

Wait for user input:

``` r
readline(prompt = 'press [enter]...')
#> press [enter]...
#> [1] ""
```

Print more digits for a number:

``` r
sprintf("%.12f",1.234343)
#> [1] "1.234343000000"
```
