Quiz 02
=======

<table>
<thead>
<tr class="header">
<th align="center">Attempts</th>
<th align="center">Score</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="center">1/3</td>
<td align="center">10/10</td>
</tr>
</tbody>
</table>

Question 01
-----------

Consider the following data with x as the predictor and y as as the
outcome.

    x <- c(0.61, 0.93, 0.83, 0.35, 0.54, 0.16, 0.91, 0.62, 0.62)
    y <- c(0.67, 0.84, 0.6, 0.18, 0.85, 0.47, 1.1, 0.65, 0.36)

Give a P-value for the two sided hypothesis test of whether
*β*<sub>1</sub> from a linear regression model is 0 or not.

### Answer

0.05296

#### Explanation

    f <- lm(y ~ x)
    summary(f)

    ## 
    ## Call:
    ## lm(formula = y ~ x)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -0.27636 -0.18807  0.01364  0.16595  0.27143 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)  
    ## (Intercept)   0.1885     0.2061   0.914    0.391  
    ## x             0.7224     0.3107   2.325    0.053 .
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.223 on 7 degrees of freedom
    ## Multiple R-squared:  0.4358, Adjusted R-squared:  0.3552 
    ## F-statistic: 5.408 on 1 and 7 DF,  p-value: 0.05296

Question 02
-----------

Consider the previous problem, give the estimate of the residual
standard deviation.

### Answer

0.223

#### Explanation

    summary(f)

    ## 
    ## Call:
    ## lm(formula = y ~ x)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -0.27636 -0.18807  0.01364  0.16595  0.27143 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)  
    ## (Intercept)   0.1885     0.2061   0.914    0.391  
    ## x             0.7224     0.3107   2.325    0.053 .
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.223 on 7 degrees of freedom
    ## Multiple R-squared:  0.4358, Adjusted R-squared:  0.3552 
    ## F-statistic: 5.408 on 1 and 7 DF,  p-value: 0.05296

Question 03
-----------

In the `mtcars` data set, fit a linear regression model of weight
(predictor) on mpg (outcome). Get a 95% confidence interval for the
expected mpg at the average weight. What is the lower endpoint?

### Answer

18.991

#### Explanation

    data(mtcars)
    x <- mtcars$wt
    y <- mtcars$mpg
    fit <- lm(y ~ x)
    predict(fit, data.frame(x = mean(x)), interval = "confidence")

    ##        fit      lwr      upr
    ## 1 20.09062 18.99098 21.19027

Question 04
-----------

Refer to the previous question. Read the help file for `mtcars`. What is
the weight coefficient interpreted as?

### Answer

The estimated expected change in mpg per 1,000 lb increase in weight.

#### Explanation

    help(mtcars)

Question 05
-----------

Consider again the `mtcars` data set and a linear regression model with
mpg as predicted by weight (1,000 lbs). A new car is coming weighing
3000 pounds. Construct a 95% prediction interval for its mpg. What is
the upper endpoint?

### Answer

27.57

#### Explanation

    predict(fit, data.frame(x = mean(3)), interval = "prediction")

    ##        fit      lwr      upr
    ## 1 21.25171 14.92987 27.57355

Question 06
-----------

Consider again the `mtcars` data set and a linear regression model with
mpg as predicted by weight (in 1,000 lbs). A "short" ton is defined as
2,000 lbs. Construct a 95% confidence interval for the expected change
in mpg per 1 short ton increase in weight. Give the lower endpoint.

### Answer

-12.973

#### Explanation

    fit2 <- lm(y ~ I(x / 2))
    tbl2 <- summary(fit2)$coefficients
    mean <- tbl2[2,1]      
    se <- tbl2[2,2] 
    df <- fit2$df
    #Two sides T-Test
    mean + c(-1,1) * qt(0.975, df = df) * se

    ## [1] -12.97262  -8.40527

Question 07
-----------

If my X from a linear regression is measured in centimeters and I
convert it to meters what would happen to the slope coefficient?

### Answer

It would get multiplied by 100.

#### Explanation

    summary(fit)$coefficients[2, 1]

    ## [1] -5.344472

    fit3 <- lm(y ~ I(x / 100))
    summary(fit3)$coefficients[2, 1]

    ## [1] -534.4472

Question 08
-----------

I have an outcome, *Y*, and a predictor, *X* and fit a linear regression
model with *Y* = *β*<sub>0</sub> + *β*<sub>1</sub>*X* + *ϵ* to obtain
$\\hat \\beta\_0$ and $\\hat \\beta\_1$. What would be the consequence
to the subsequent slope and intercept if I were to refit the model with
a new regressor, *X* + *c* for some constant, *c*?

### Answer

The new intercept would be $\\hat \\beta\_0 - c \\hat \\beta\_1$.

Question 09
-----------

Refer back to the mtcars data set with mpg as an outcome and weight (wt)
as the predictor. About what is the ratio of the the sum of the squared
errors, $\\sum\_{i=1}^n (Y\_i - \\hat Y\_i)^2$ when comparing a model
with just an intercept (denominator) to the model with the intercept and
slope (numerator)?

### Answer

0.25

#### Explanation

    fitRes <- fit$residuals ^ 2
    fitIntercept <- lm(mpg ~ 1, mtcars)
    fitInterceptRes <- fitIntercept$residuals ^ 2
    sum(fitRes) /sum(fitInterceptRes)

    ## [1] 0.2471672

Question 10
-----------

Do the residuals always have to sum to 0 in linear regression?

### Answer

If an intercept is included, then they will sum to 0.
