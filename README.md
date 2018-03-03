
<!-- README.md is generated from README.Rmd. Please edit that file -->
R-miscellany
------------

A collection of useful R code bits I'm tired of looking up.

Data reading and writing
------------------------

Data manipulation
-----------------

Drop columns from data frame by name:

``` r
iris[!colnames(iris) %in% c("Sepal.Length","Sepal.Width")]
```

Timestamps
----------

Plotting
--------

Four plots in one graph:

``` r
par(mfrow=c(2,2))
```
