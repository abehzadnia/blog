---
title: "Probability Function"
author: Alireza Behzadnia
date: '2018-03-11'
slug: probability_function

categories:
  - Statistics
  - Probability
tags:
  - Statistics
  - Probability
  - PMF
  - PDF

weight: 100

toc: true
---

Probability function is the function of a random variable distribution, whose value provides the *absolute* or *relative likelihood* of the value of the random variable in the sample.

<!--more-->
Depending on the *type* of the random variable, we can calculate:

  - **Absolute likelihood** for a <u>discrete variable</u>
  - **Relative likelihood** for a <u>continuous variable</u>

On this page we will discuss:

  - [Probability Mass Function](#probability-mass-function)
  - [Probability Density Function](#probability-density-function)
  - [Popular PMFs and PDFs](#pmfs-and-pdfs)

## Probability Mass Function
Discrete random variables have discrete and countable values (e.g. white cell count). **Probability Mass Function**, is a function which assigns the probability of a random variable taking a certain value. For example, a coin toss.

Assume a simple random experiment: a **fair** coin is tossed twice. Let $ X $ be the number of tails we get:

  - $ S = {(HH),(TH),(HT),(TT)} $
  - P(X = 0) = (HH)
  - P(X = 1) = (HT) or (TH)
  - P(X = 2) = (TT)

Here we can use a binomial distribution to calcualte the **absolute** likelihood of (X = 2) using the Probability Mass Function for binomial distributions:

$$ P\left(X = k~|~~ n = n, p= p\right) = ^nC\_k \ p^k (1-p)^{n-k} $$


Here we can calculate the P(X = k) for each outcome:

```r
dbinom(0, 2, 0.5)
```

```
## [1] 0.25
```

```r
dbinom(1, 2, 0.5)
```

```
## [1] 0.5
```

```r
dbinom(2, 2, 0.5)
```

```
## [1] 0.25
```

Since *Probability Mass Function* gives the probability of *discrete* data, we can visualize the probability distribution using histograms. Though the result may not be impressive when our sample size is rather small.


```r
Two_cointosses_5_times = sample(x=c("HH","HT","TT"), size=5, replace = T, prob=c(.25,.50,.25))
barplot(table(Two_cointosses_5_times))
```

<img src="/post/statistics/probability/probability_function_files/figure-html/unnamed-chunk-2-1.png" width="672" />


Let's see what will happen if we repeat this experiment 1000 times:


```r
Two_cointosses_1000_times = sample(x=c("HH","HT","TT"), size=1000, replace = T, prob=c(.25,.50,.25))
barplot(table(Two_cointosses_1000_times))
```

<img src="/post/statistics/probability/probability_function_files/figure-html/unnamed-chunk-3-1.png" width="672" />

The area under the histogram equals $ 1 $ (since the sum of P(X = x) = 1) and the area of each ~*bar*~ is the probability of given outcome. More precisely the area of each bin equals to finding a binomial variable with a value euqal to the one at the centred of its respective bin.


## Probability Density Function

In contrast, the normal distribution also called the *Gaussian* distribution can take any numerical value between negative infinity and positive infinity. Since it can take a continuum of values,it is a continuous random variable.

Consider random variable X = foot length of adult males. Unlike shoe size, this variable is not limited to distinct, separate values (i.e. It is not discrete), because foot lengths can take any value over a continuous range of possibilities, so we cannot present this variable with a probability histogram or a table.

The probability distribution of foot length (or any other continuous random variable) can be represented by a smooth curve called a **probability density curve**.
![](/probability/pdf.gif)
The total area under the density curve equals 1, and the curve represents probabilities by area.


When the random variable is continuous, it has *probability zero of taking any single value*, `\(P(X =x) =0\)`. Here we can only talk about the **relative likelihood** of the continuous random variable *within some interval*. Continuous random variables have **probability density functions** or pdfs instead of probability mass functions.
![](/probability/pdf2.gif)

The PDF curve of a random variable `\(X\)` with `\(M =\mu\)` and `\(SD = \sigma\)`:
$$\large f(x)=\frac{1}{\sigma\sqrt{2\pi}}~\times~ e^{\LARGE[-\frac{1}{2\pi^2}\times(x-\mu)^2]} $$

Here the area under the curve, or the **density** would be:
$$ P( a \leq x \leq b) = \int_{a}^{b}f(x)dx$$

## PMFs and PDFs
There are many types of PMFs and PDFs, here are a handful of most famous distributions:

  - Discrete (*PMF*)
    - Binomial
    - Poisson
  - Continuous (*PDF*)
    - Normal distribution
    - Uniform
    - Beta
    - Gamma
