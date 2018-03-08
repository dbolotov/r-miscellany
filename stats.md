
-   [Statistics miscellany](#statistics-miscellany)

<!-- stats.md is generated from stats.Rmd Please edit that file -->
### Statistics miscellany

#### ANOVA

[video source](https://www.youtube.com/watch?v=fT2No3Io72g)

``` r
Group1 <- c(2,3,7,2,6)
Group2 <- c(10,8,7,5,10)
Group3 <- c(10,13,14,13,15)

Combined_Groups <- data.frame(cbind(Group1, Group2, Group3))
Stacked_Groups <- stack(Combined_Groups)
Anova_Results <- aov(values ~ ind, data = Stacked_Groups)
summary(Anova_Results)
```
