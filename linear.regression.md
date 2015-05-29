Linear regression
========================================================
author: Maria Paniw

date: 27.5.2015


Regression
========================================================
Regression analyzes relationships between continuous variables,
i.e., variables that can go from $-\infty$ to  $\infty$

Basically, regression analysis describes the relationship between the predictor (*x*-axis) and the response (*y*-axis)

R uses the function `lm()` for linear regression analysis


Defining a straight line
========================================================

Regression, as any kind of statistical analysis, begins with a hypothesis:

> Hypothesis: Variable X drives the response Y. 

Once we have our hypothesis, we must express it mathematically.

![equation] (http://www.sciweavers.org/download/Tex2Img_1432887339.jpg)

What kind of ![] (http://www.sciweavers.org/download/Tex2Img_1432887381.jpg)?

In linear regression: Y is a linear function of X, i.e.,

![] (http://www.sciweavers.org/download/Tex2Img_1432887440.jpg)
 


Defining parameters
========================================================

Here, ![] (http://www.sciweavers.org/download/Tex2Img_1432887480.jpg) is the **intercept** and ![] (http://www.sciweavers.org/download/Tex2Img_1432887536.jpg) is the **slope** 

These are the two **parameters** of our linear model.

If the parameters are known, and our data can be entirely described by the linear
relationship between X and Y, we have a deterministic function:

Deterministic relationship between X and Y 
========================================================


```r
determ.lf = function(x) 3 + 2.5*x

x.vec = c(c(-1:20))
```

Plot the relationship
=====


```r
plot(x=x.vec,y=determ.lf(x=x.vec),type="l", ylab="Y")

abline(h=3,col="red")
```
![Regression plot](G:/Teaching/StatCourse/Presentations/week1_regression-figure/unnamed-chunk-2-1.png) 

Statistical relationship between X and Y 
========================================================

![Random points](G:/Teaching/StatCourse/Presentations/week1_regression-figure/unnamed-chunk-3-1.png) 

Statistical relationship between X and Y 
========================================================
If we cannot predict our data excatly by the linear regression because we have
variation in our data that is not accounted for, we turn to a statistical model

![] (http://www.sciweavers.org/download/Tex2Img_1432887589.jpg)

Each observation *i* in our data (*rows*), is associated with a value for X and Y, both measured at the same replicate! 

The betas and the epsilon
========================================================

![] (http://www.sciweavers.org/download/Tex2Img_1432887480.jpg) and  ![] (http://www.sciweavers.org/download/Tex2Img_1432887536.jpg) are  constants 

On the other hand, ![] (http://www.sciweavers.org/download/Tex2Img_1432887703.jpg)

![] (http://www.sciweavers.org/download/Tex2Img_1432887746.jpg) is the variance, which is 0 if the points lie perfectly on the line. 

So what's the deal with normality?
========================================================

When you do linear regression, you are always asked:

> Is Y normally distributed? 

This is because, shifting the equation for linear regression a bit: 

![] (http://www.sciweavers.org/download/Tex2Img_1432887782.jpg)


The points make the variance
========================================================
The more spread out the points, the larger $\sigma^2$

In plot 1, ![] (http://www.sciweavers.org/download/Tex2Img_1432887703.jpg) is larger than in plot 2


![Regression plot 2](G:/Teaching/StatCourse/Presentations/week1_regression-figure/unnamed-chunk-4-1.png) 


If points have a noise component, how do we fit a line?
========================================================

The key concept of linear regression:

The residual sum of squares!

![] (http://www.sciweavers.org/download/Tex2Img_1432887841.jpg)

where ![] (http://www.sciweavers.org/download/Tex2Img_1432887870.jpg) is the observed repsonse at point *i* and ![] (http://www.sciweavers.org/download/Tex2Img_1432888183.jpg) is the predicted value from the regression equation.

The **best fit** regression line minimizes RSS.

How doe we estimate the two parameters in the model?
========================================================

The sum of squares of a variable X ($SS_X$) measures the squared deviation of each observation $X_i$ from the mean of all the observations $\bar X$ :

! [] (http://www.sciweavers.org/download/Tex2Img_1432888224.jpg)

Dividing this SS by (*n*-1), where *n* is our sample size, gives us the sample variance:

![] (http://www.sciweavers.org/download/Tex2Img_1432888343.jpg)


In a linear regression, we have at least two variables of course
========================================================

Thus, we have to measure the sample covariance! 

In this case, we have a **sum of cross products**: 

![] (http://www.sciweavers.org/download/Tex2Img_1432888390.jpg)

Which, divided by (*n*-1), gives us the sample **covariance**:

![] (http://www.sciweavers.org/download/Tex2Img_1432888864.jpg)

The slope and intercept
========================================================

![] (http://www.sciweavers.org/download/Tex2Img_1432887480.jpg) and ![] (http://www.sciweavers.org/download/Tex2Img_1432887536.jpg) are the estimated as:

![] (http://www.sciweavers.org/download/Tex2Img_1432888958.jpg)

and 

![] (http://www.sciweavers.org/download/Tex2Img_1432889001.jpg)

The error term
========================================================

The last thing we need to estimate is ![] (http://www.sciweavers.org/download/Tex2Img_1432889158.jpg).

Remember that ![] (http://www.sciweavers.org/download/Tex2Img_1432889197.jpg)

So, we need an estimate of ![] (http://www.sciweavers.org/download/Tex2Img_1432889228.jpg) to get ![] (http://www.sciweavers.org/download/Tex2Img_1432889158.jpg):

![equation] (http://www.sciweavers.org/download/Tex2Img_1432886948.jpg)
SS as fundamental principle of parametric analyses
========================================================

In parametric analysis, we want to partition the SS (sum of squares) into different components. 

Conceptually, we are looking at our response, *Y*, and $SS_Y =  \sum\limits_{i=1}^n (Y_i - \bar Y_i)^2$ is the total variance that we are trying to partition into its components:

The *RSS* is the  random component. The remaining variation, $SS_{reg}$, is the regression relatioship $Y_i = \beta_0 + \beta_1X_i$

So, the total variance is: $SS_Y = SS_{reg} + RSS$


Is the relationship between X and statistically significant?
========================================================

$H_0:$ $Y_i = \beta_0 + \epsilon_i$

$H_a:$ $Y_i = \beta_0 + \beta_1X_i + \epsilon_i$


Welcome to the world of ANOVA
========================================================

![ANOVA table](ANOVAtable.png)
Source: Gotelli & Ellison (2004)