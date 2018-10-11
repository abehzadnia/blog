---
title: Survival Analysis (introduction)
date: 2018-10-05T00:00:00.000Z
author: Alireza Behzadnia
slug: sa_introduction
categories:
  - Statistics
  - survival
tags:
  - Statistics
  - Survival Analysis
weight: 500
---

After two months of living data-mania-less-ness-ly, I finally got my hands on a small cohort data! Alas! This was going to be my first survival analysis project that I was responsible for. I seized this opportunity to blog about a n00b's take on SA.

# Survival Analysis

Survival Analysis (SA) is a time to event analysis of cases, where an event is pre-defined (e.g. remission, death, payment of a mortgage etc). Every case is followed up until:

1. Event (failure) has occurred
2. End point of follow up has reached
3. Case was lost to follow up.

Observations would either be censored (2 and 3) or are considered as a failure (failure can also be a good thing! like in cancer remission).

Survival analysis is a convenient tool when modelling is not suitable - one of its many advantages.

{{

<mermaid align="center">}}
graph LR;
    A(Population of interest) --&gt; B(Sampling)
    B --&gt;C(Data)
{{&lt; /mermaid &gt;}}</mermaid>

{{

<mermaid align="center">}}
graph LR;
    A(Data) --&gt; |EDA| B{Analysis}
    A --&gt; C((Model <br> imposition))
    C --&gt; |Bayesian|D(Prior probability <br> or distribution)
    C --&gt; |Frequentist|B
    D --&gt; B
    B --&gt; |EDA|E((Inferential <br> modeling))
    B --&gt; |Bayesian and <br> Frequenstist|F(Conclusion)
    E --&gt; F
{{&lt; /mermaid &gt;}}</mermaid>

{{

<mermaid align="center">}}
graph LR;
    H(Conclusion) --&gt; |Bayesian|G(Updating priori <br> using the posteriori)
{{&lt; /mermaid &gt;}}</mermaid>
