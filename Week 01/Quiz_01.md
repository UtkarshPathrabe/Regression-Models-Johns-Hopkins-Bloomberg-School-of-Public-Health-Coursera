Quiz 01
=======

| Attempts | Score |
|:--------:|:-----:|
|    1/3   | 10/10 |

Question 01
-----------

Consider the data set given below:

``` r
x <- c(0.18, -1.54, 0.42, 0.95)
```

And weights given by:

``` r
w <- c(2, 1, 3, 1)
```

Give the value of \(\(\mu\)\) that minimizes the least squares equation \(\(\sum_{i=1}^n w_i (x_i - \mu)^2\)\)

### Answer

0.1471

#### Explanation

``` r
weighted.mean(x, w)
```

    ## [1] 0.1471429

Question 02
-----------

Consider the following data set:

``` r
x <- c(0.8, 0.47, 0.51, 0.73, 0.36, 0.58, 0.57, 0.85, 0.44, 0.42)
y <- c(1.39, 0.72, 1.55, 0.48, 1.19, -1.59, 1.23, -0.65, 1.49, 0.05)
```

Fit the regression through the origin and get the slope treating y as the outcome and x as the regressor. (Hint, do not center the data since we want regression through the origin, not through the means of the data.)

### Answer

0.8263

#### Explanation

``` r
lm(y ~ x - 1)
```

    ## 
    ## Call:
    ## lm(formula = y ~ x - 1)
    ## 
    ## Coefficients:
    ##      x  
    ## 0.8263

Question 03
-----------

Do `data(mtcars)` from the datasets package and fit the regression model with mpg as the outcome and weight as the predictor. Give the slope coefficient.

### Answer

-5.344

#### Explanation

``` r
data(mtcars)
lm(mpg ~ wt, mtcars)
```

    ## 
    ## Call:
    ## lm(formula = mpg ~ wt, data = mtcars)
    ## 
    ## Coefficients:
    ## (Intercept)           wt  
    ##      37.285       -5.344

Question 04
-----------

Consider data with an outcome (Y) and a predictor (X). The standard deviation of the predictor is one half that of the outcome. The correlation between the two variables is .5. What value would the slope coefficient for the regression model with <b><i>Y</i></b> as the outcome and <b><i>X</i></b> as the predictor?

### Answer

1

#### Explanation

``` r
corOfYandX <- 0.5
sdYoverX <- 2
corOfYandX*sdYoverX
```

    ## [1] 1

Question 05
-----------

Students were given two hard tests and scores were normalized to have empirical mean 0 and variance 1. The correlation between the scores on the two tests was 0.4. What would be the expected score on Quiz 2 for a student who had a normalized score of 1.5 on Quiz 1?

### Answer

0.6

#### Explanation

``` r
corOfYandX <- 0.4
quiz1 <- 1.5
quiz1*corOfYandX*1 + 0
```

    ## [1] 0.6

Question 06
-----------

Consider the data given by the following:

``` r
x <- c(8.58, 10.46, 9.01, 9.64, 8.86)
```

What is the value of the first measurement if x were normalized (to have mean 0 and variance 1)?

### Answer

-0.9719

#### Explanation

``` r
mean <- mean(x)
sd <- sd(x)
(x[1] - mean)/sd
```

    ## [1] -0.9718658

Question 07
-----------

Consider the following data set (used above as well). What is the intercept for fitting the model with x as the predictor and y as the outcome?

``` r
x <- c(0.8, 0.47, 0.51, 0.73, 0.36, 0.58, 0.57, 0.85, 0.44, 0.42)
y <- c(1.39, 0.72, 1.55, 0.48, 1.19, -1.59, 1.23, -0.65, 1.49, 0.05)
```

### Answer

1.567

#### Explanation

``` r
lm(y ~ x)
```

    ## 
    ## Call:
    ## lm(formula = y ~ x)
    ## 
    ## Coefficients:
    ## (Intercept)            x  
    ##       1.567       -1.713

Question 08
-----------

You know that both the predictor and response have mean 0. What can be said about the intercept when you fit a linear regression?

### Answer

It must be identically 0.

Question 09
-----------

Consider the data given by:

``` r
x <- c(0.8, 0.47, 0.51, 0.73, 0.36, 0.58, 0.57, 0.85, 0.44, 0.42)
```

What value minimizes the sum of the squared distances between these points and itself?

### Answer

0.573

#### Explanation

``` r
mean(x)
```

    ## [1] 0.573

Question 10
-----------

Let the slope having fit Y as the outcome and X as the predictor be denoted as \(\(\beta_1 \)\). Let the slope from fitting X as the outcome and Y as the predictor be denoted as \(\(\gamma_1 \)\). Suppose that you divide \(\(\beta_1 \)\) by \(\(\gamma_1 \)\), in other words consider \(\(\beta_1 / \gamma_1\)\). What is this ratio always equal to?

### Answer

Var(Y) / Var(X)

#### Explanation

``` r
cor(X, Y)*sd(Y)/sd(X) / (cor(X,Y)*sd(X)/sd(Y))
= sd(Y)^2/(sd(X)^2) 
= var(Y)/var(X)
```
