
-   [ANOVA](#anova)
-   [Line and curve fitting](#line-and-curve-fitting)

<!-- stats.md is generated from stats.Rmd Please edit that file -->
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

#### Line and curve fitting

Fit a line to series of points

``` r
#data
m <- 5
n <- 2
input <- matrix(c(1, 6, 2, 5, 3, 7, 4, 10, 5, 14), ncol = n, byrow = T)
k <- rep(1,m)
X <- cbind(k, input[,1])
y <- input[,2]

X.T <- t(X)
betaHat <- solve(X.T%*%X) %*% X.T %*%y
print(betaHat)
plot(input)
abline(betaHat[1], betaHat[2])
```

Fit a 2nd degree polynomial to series of points

``` r
X <- cbind(rep(1,m), input[,1], (input[,1])^2)
y <- input[,2]
X.T <- t(X)
betaHat <- solve(X.T%*%X) %*% X.T %*%y
print(betaHat)
plot(input)

#plot curve beyond original data
num_points <- 10
new_X <- c(1:num_points)
new_poly <- cbind(rep(1,num_points),new_X,new_X^2)
plot(x = new_X, y = new_poly%*%betaHat,col='red')
lines(input)
```
