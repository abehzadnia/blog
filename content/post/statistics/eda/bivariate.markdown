---
title: "Bivariate Analysis"
date: 2018-04-11
author: Alireza Behzadnia
slug: eda_bivariate_analysis
categories:
  - Statistics
  - EDA
tags:
  - EDA
  - Descriptive
  - Statistics
  - Bivariate Analysis

weight: 10

toc: true

---
**Bivariate analysis** explore the possible relationship between two variables' variability. In view of "**exploratory**" focus of EDA, we should refrain from infering based on bivariate analysis.

<!--more-->
## Covariance
Covariance examines the joint varaince of two variables. In univariate analysis we looked at measures of: **centre**, **spread** and **skewness**. Comparing means at the EDA stage is as simple as calculating seperate means for each variable while *refraining* from inference!

Covariance between two varaiables `\(X\)` and `\(Y\)` can be calculated as:

`$$Cov[XY] = \sigma_XY = E\ [\ (X - \overline{X})\ (Y - \overline{Y})\ ] \\ \ \\ = \frac{1}{N - 1} \sum_{i = 1}^{N}(x_i - \overline{X})(y_i - \overline{Y})$$`

Covariance is a generalised version of the variance formula. For example, for a single variable we'd have `\(Cov[XX] = E\ [\ (X - \overline{X})^2\ ] = Var[X]\)`.

{{% expand "Example" %}}

```r
library(MASS)
data("leuk")
leuk$rbc <- (leuk$wbc * 4)/10 + 2 # making up a new
var(leuk$wbc)
```

```
## [1] 1189517888
```

```r
var(leuk$rbc)
```

```
## [1] 190322862
```

```r
cov(leuk$rbc, leuk$wbc) #lower Var in RBc has pulled down the joint variability
```

```
## [1] 475807155
```

{{% /expand %}}


## Correlation coefficient
Correlation coefficient measures the strength of the relationship.
`$$CC_xy = \rho_xy = \frac{\sigma_xy}{\sigma_x \sigma_y} = \frac{1}{N-1} \sum_{i = 1}^{N} \frac{(x_i - \overline{X})}{\sigma_x} \frac{(y_i - \overline{Y})}{\sigma_y}$$`

The formula is the same for `\(r_xy\)` - as in the sample statistics rather than the population ( `\(\rho_xy\)` ). CC value ranges from -1 to 1, determining the relative **strength** and **direction** of the relationship.


```r
cor(leuk$wbc, leuk$time)
```

```
## [1] -0.3294525
```


## Rank correlation coefficient
Correlation coefficient as defined above is also known as **Pearson r**. Pearson CC assumes a *linear* relationsip. If we were interested in *non-linear* relationship between two variables, we would need to use **Rank Correlation Coefficient (RCC)** commonly known as **Spearman r**.

In RCC each variable is first sorted and then transformed as such that the smallest data point is ranked = 1 and the largest Nth is ranked = n. This is known as *rank transformation*. We would then calcualte the CC of the ranked variables rather than the raw data points.


`$$RCC_xy = \rho_xy(rank) = \frac{\sigma_xy(rank)}{\sigma_x(rank) \sigma_y(rank)} = \frac{1}{N-1} \sum_{i = 1}^{N} \frac{(R_{x,i} - \overline{R}_x)}{\sigma_x(rank)} \frac{(R_{y,i} - \overline{R}_y)}{\sigma_y(rank)}$$`

The prefix *R* denotes rank transformed values.


```r
cor(leuk$wbc, leuk$time, method = "spearman")
```

```
## [1] -0.4986164
```

{{% notice tip %}} **Spearman r** and **Pearson r** should usually be carried out together to assess the robustness of the CC.
Spearman coefficient is more resistant to outliers (*robust measure of correlation*). As we are not dealing with values rather the rank transformed data, outliers would not influence our correlation.
{{% /notice %}}


```r
a <- c(leuk$wbc, 1*10^10)
b <- c(leuk$time, 10)

cor(leuk$wbc, leuk$time)
```

```
## [1] -0.3294525
```

```r
cor(a, b) # a huge reduction in our correlation strength
```

```
## [1] -0.114399
```

```r
cor(leuk$wbc, leuk$time, method = "spearman")
```

```
## [1] -0.4986164
```

```r
cor(a, b, method = "spearman") # only a slight difference
```

```
## [1] -0.4934468
```

## Graphical analysis
The best way to visualise the relationship between two sets of numerical variable is in fact using a scatter plot.


```r
attach(leuk)
plot(rbc, wbc)
```

<img src="/post/statistics/eda/bivariate_files/figure-html/unnamed-chunk-5-1.png" width="672" />

Let's look at the utility of rank transformation:

```r
attach(Theoph)
plot(Time, conc) # doesn't look good, look at the cluster of outliers
```

<img src="/post/statistics/eda/bivariate_files/figure-html/unnamed-chunk-6-1.png" width="672" />

```r
plot(rank(Time), rank(conc)) # much better looking, we can see the Theophylline concentration increases and then decreases (due to its half life)
```

<img src="/post/statistics/eda/bivariate_files/figure-html/unnamed-chunk-6-2.png" width="672" />


## Multivariate analysis
Multivariate analysis involves calculating the CC for each pair of variables we have at hand. The result would be a matrix of correlation coefficients.


```r
cor(subset(leuk, select = c(wbc, rbc, time)))
```

```
##             wbc        rbc       time
## wbc   1.0000000  1.0000000 -0.3294525
## rbc   1.0000000  1.0000000 -0.3294525
## time -0.3294525 -0.3294525  1.0000000
```

```r
pairs(leuk)
```

<img src="/post/statistics/eda/bivariate_files/figure-html/unnamed-chunk-7-1.png" width="672" />

## Categorical variables
So far our focus has been on numerical variables. But what if we are working with categorical variables? When working with categorical variables we can either have two categorical variables or one categorical variable.

### Categorical and Quantitative
Let's assume we have a categorical explanatory variable and a quantitative response variable.

We will use the data from Cushny, A. R. and Peebles, A. R. (1905) The action of optical isomers: II hyoscines in `sleep` data set.


```r
data(sleep)
str(sleep)
```

```
## 'data.frame':	20 obs. of  3 variables:
##  $ extra: num  0.7 -1.6 -0.2 -1.2 -0.1 3.4 3.7 0.8 0 2 ...
##  $ group: Factor w/ 2 levels "1","2": 1 1 1 1 1 1 1 1 1 1 ...
##  $ ID   : Factor w/ 10 levels "1","2","3","4",..: 1 2 3 4 5 6 7 8 9 10 ...
```

We can see that our explanatory variable is `Group`. Let's say Group 1 is the control group 2 is the treatment group. Our response variable (Y-axis) is `extra` sleep measured in hours.

We can look at the statistics of the two groups:

```r
tapply(sleep$extra, sleep$group, summary)
```

```
## $`1`
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
##  -1.600  -0.175   0.350   0.750   1.700   3.700
##
## $`2`
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
##  -0.100   0.875   1.750   2.330   4.150   5.500
```

A more elegant way of doing this is to use the `dplyr` package:

```r
library(dplyr)
sleep %>%
  group_by(group) %>%
  summarise(mean = mean(extra), median = median(extra), sd = sd(extra), IQR = IQR(extra))
```

```
## # A tibble: 2 x 5
##   group  mean median    sd   IQR
##   <fct> <dbl>  <dbl> <dbl> <dbl>
## 1 1     0.750  0.350  1.79  1.88
## 2 2     2.33   1.75   2.00  3.28
```

We can use graphical analysis to visualise the difference too:

```r
attach(sleep)
boxplot(extra, group)
```

<img src="/post/statistics/eda/bivariate_files/figure-html/unnamed-chunk-11-1.png" width="672" />

We can't use scatterplot to visualise this however!

### Categorical and Catagorical variable
In this case we can only compare the relative frequency and portions in each group. Let's look at the data from case-control study of esophageal cancer in France:

```r
data("esoph")
str(esoph)
```

```
## 'data.frame':	88 obs. of  5 variables:
##  $ agegp    : Ord.factor w/ 6 levels "25-34"<"35-44"<..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ alcgp    : Ord.factor w/ 4 levels "0-39g/day"<"40-79"<..: 1 1 1 1 2 2 2 2 3 3 ...
##  $ tobgp    : Ord.factor w/ 4 levels "0-9g/day"<"10-19"<..: 1 2 3 4 1 2 3 4 1 2 ...
##  $ ncases   : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ ncontrols: num  40 10 6 5 27 7 4 7 2 1 ...
```

Here `age group` and `tobacco consumption (gm/day)` are two categorical variables. We can tabulate these two:


```r
table1 <- table(esoph$agegp, esoph$tobgp)
table1
```

```
##        
##         0-9g/day 10-19 20-29 30+
##   25-34        4     4     3   4
##   35-44        4     4     4   3
##   45-54        4     4     4   4
##   55-64        4     4     4   4
##   65-74        4     4     4   3
##   75+          4     4     1   2
```

We can ask the question **what portion of 45 to 54 ages individuals smoke 20-29g of tobacco per day:**


```r
prop.table(table1, 1)*100
```

```
##        
##          0-9g/day     10-19     20-29       30+
##   25-34 26.666667 26.666667 20.000000 26.666667
##   35-44 26.666667 26.666667 26.666667 20.000000
##   45-54 25.000000 25.000000 25.000000 25.000000
##   55-64 25.000000 25.000000 25.000000 25.000000
##   65-74 26.666667 26.666667 26.666667 20.000000
##   75+   36.363636 36.363636  9.090909 18.181818
```

We can see that 25% of the 45-54 years group smoke 20-29g per day.

Question 2: **Among those who smoke 20-29g per day, what percentage of them are 45 to 54 years of age?**

```r
prop.table(table1, 2)*100
```

```
##        
##         0-9g/day    10-19    20-29      30+
##   25-34 16.66667 16.66667 15.00000 20.00000
##   35-44 16.66667 16.66667 20.00000 15.00000
##   45-54 16.66667 16.66667 20.00000 20.00000
##   55-64 16.66667 16.66667 20.00000 20.00000
##   65-74 16.66667 16.66667 20.00000 15.00000
##   75+   16.66667 16.66667  5.00000 10.00000
```

20% of those who smoke 20-29g per day, are 45-54 years old.

Graphically we can use **barplots** to analyse categorical variables:

```r
library(ggplot2)
ggplot(esoph, aes(x = agegp, fill = tobgp)) +
  geom_bar()
```

<img src="/post/statistics/eda/bivariate_files/figure-html/unnamed-chunk-16-1.png" width="672" />
