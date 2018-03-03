
-   [R-miscellany](#r-miscellany)
-   [Data reading and writing](#data-reading-and-writing)
-   [Data manipulation](#data-manipulation)
-   [Timestamps](#timestamps)
-   [Plots](#plots)
-   [Rmarkdown template](#rmarkdown-template)

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

Plots
-----

Four plots in one graph:

``` r
par(mfrow=c(2,2))
```

Rmarkdown template
------------------

``` text
# ---
# title: "BD Basecamp - Best Models to PMML: Stockout Percent"
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
