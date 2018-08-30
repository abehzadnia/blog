---
title: "Discrete Probability Distribution"
author: Alireza Behzadnia
date: '2018-03-12'
slug: probability_discrete_distribution
categories:
  - Statistics
  - Probability
tags:
  - Statistics
  - Probability
  - Discrete distribution
  - PMF
  - Bernoulli
  - Poisson
  - Binomial

weight: 2
---

Probability distributions demonstrate the probability of an event. When dealing with discrete data, **probability mass function** of the *event* can come from various distributions. The most important discrete probability distributions are the **Bernoulli**, **Binomial** and **Poisson**.

<!--more-->

***
## Bernoulli distribution
The most widely known _unknown_ discrete probability distribution is the **Bernoulli distribution**.

Named after the Swiss mathematician [Jacob Bernoulli](https://en.wikipedia.org/wiki/Jacob_Bernoulli), the Bernoulli distribution is the probability distribution of the outcome of a single experiment with two possible outcomes. Each outcome is a Boolean-valued discrete random variable (*k=1* or *k=0*).

Unlike the binomial distribution, the Bernoulli distribution is used in **single trial (n=1)** experiments. This is a special case of the Binomial distribution where a single experiment/trial is conducted (n=1).

$ X $ is a discrete random variable that belongs to the Bernoulli distribution if:
$$ P(X=1) = p = 1 - P(X = 0) = 1 - q $$

### Bernoulli Probability Mass Function
The probability mass function can be written as:

<div>$$ f(k;p) = \left\{ \begin{array}{lcl}p &\mbox{if}&k=1 \\ 1-p &\mbox{if}&k=0 \end{array} \right. $$</div>

Can be expressed as:

$$ f(k;p) = p^k(1-p)^{1-k} ~for~k\in \{0,1\}  $$



***
A **binomial variable** of parameters (n,p) is the **sum of $ n $ Bernoulli variables** of parameter p.

***

#### Example
While focusing on locating the NPHLM gene, the [Kehjistanian](http://diablo.wikia.com/wiki/Kehjistan) scientists also discovered that, for any given birth at any given day, there is a fixed 0.60 chance that the newborn is a female.

If on average there is one birth every 2 minutes, what is the projected population of males in Caldeum over 20 years?

```r
n = (60*24*365*20)/2
x = sample(c(0,1), n, replace=T, prob=c(.6,.4))
```


```r
plot(cumsum(x), type='l',
     main="Cummulative sums of males (a Bernoulli variable)")
```

<img src="/post/statistics/probability/pmf_files/figure-html/unnamed-chunk-2-1.png" width="672" />

## Binomial distribution

The binomial distribution describes the probability of having exactly ___k___ successes in ___n___ independent Bernoulli trials, given that the probability of _k = 1_ is ___p___. It is important to note that the success rate of the binary event remains constant for all n independent trials.

To use a binomial distribution, data must come from a **binomial experiment**:

- $ n $ = fixed number of trials
- Trials must be **independent**
- Each trial has **two possible outcome** where:
    - *P*(sucess) = constant for each trial
    - *P*(failure) = 1 - *P*(sucess)

Given the requirements are met, the probability distribution of our binary event has a mean of $ np $ and variance of $ np(1-p) $

### Example
Kehjistanian scientists have identified the gene NPHLM on the locus 14p.61 which predisposes children to a certain lifestyle.

It is estimated that 1 in 40 child under the age of 16 have this mutation. According to the last census at [Caldeum](http://diablo.wikia.com/wiki/Caldeum), number of kids under 16 is roughly 400,000.

A sample of 200 has been collected. How many children with NPHLM mutation can we expect to find?


```r
N = 400000
n = 200
p = 1/40
x = rep(0,N)
```


```r
for (i in 1:N){{
  x[i] = sum(runif(n)<p)
}}
hist(x, main = "Distribution of NPHLM mutation in a sample of 200")
```

<img src="/post/statistics/probability/pmf_files/figure-html/unnamed-chunk-4-1.png" width="672" />
