```r

# Ecological/Biological Statistics with R
# Maria Paniw
# Week 1: Linear regression

# Load the data (change the directory to your own or import dataset manually from the environment tab in RStudio)

data=read.csv("G:/Teaching/StatCourse/Presentations/sizeDroso.csv") 

# We want to estimate whether there is a significant relationship between size and sizeNext,
# ignoring the two sites (for now)


# To estimate the intercept and slope, we need the variance and covariance components

# First get rid of all the NA in the data

data.sub=data[!is.na(data$size)&!is.na(data$sizeNext),]

# Now, let's take the means of the varaibles in question:

meanX=mean(data.sub$size)

meanY=mean(data.sub$sizeNext)

n <- nrow(data.sub)
SSy <- sum((data.sub$sizeNext - meanY)^2)
s.y2 <- SSy/(n - 1)
SSxy <- sum((data.sub$sizeNext - meanY) * (data.sub$size - meanX))
s.xy <- SSxy/(n - 1)
s.x2 <- sum((data.sub$size - meanX)^2)/(n - 1)

# The slope! 

beta1 <- s.xy/s.x2

beta1

#The intercept

beta0 <- meanY - (beta1 * meanX)

beta0

# The residual variance

RSS <- sum((data.sub$sizeNext - (beta0 + beta1 * data.sub$size))^2)
RMS <- RSS/(n - 2)
RMS.sterr <- sqrt(RMS) # standard error of the residual mean square
RMS
RMS.sterr

# Now, all we need for the ANOVA table is 

SSreg <-sum(((beta0 + beta1 * data.sub$size)- meanY)^2)

r2 <- SSreg/SSy

# Now we can get the F ratio

Fratio <- (SSreg/1)/(RSS/(n - 2))

# Don't have an F statistic table handy to see if F ratio is statistically significant
# no problem:

# create a random density distribution of the F distribution with 1st degree of freedom = 1,
# and 2nd degree of freedom = n-2 = 133

Fdens=density(rf(n = 1000, df1 = 1, df2 = n - 2))

#Plot the F density and the Fratio that we get by diving SSreg/RSS
plot(Fdens, 
     xlim = c(0,Fratio + 5), main = "", xlab = "F-value")
title("Distribution F with df(1, 133)")
abline(v = Fratio, lwd = 2, lty = 3)

##################################
# Of course, you can easily do all the steps above in R with the function lm

# Run lm in R

data.lm = lm(formula=sizeNext~size,data=data)

# what is the new object data.lm made of?

str(data.lm)

# get the coefficients (which are our two parameters )

data.lm$coefficients

#Compare with:
beta0; beta1

# Get the summary statistics of the linear model
summary(data.lm)

#Compare with:
sterror
Fratio
r2 
# get the familiar ANOVA table

anova(data.lm)
RMS
SSreg



```
