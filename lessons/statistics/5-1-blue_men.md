[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

---

## Problem Statement
In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters µ = 178 cm and σ = 7.7 cm for men, and µ = 163 cm and σ = 7.3 cm for women.

In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf.

---

#### Steps to solve the problem
[1)  Import required libraries and packages](#section-a)  
[2)  Define Mu, Sigma, and Normal Distribution](#section-b)  
[3)  Calculate Percentages Using Distribution](#section-c)  

---

## <a name="section-a"></a> 1. Imports

```{python}
import scipy.stats
```
---

## <a name="section-b"></a> 2. Normal Distribution
```{python}
#scipy.stats.norm represents a normal distribution
distribution = scipy.stats.norm(mu, sigma)
```

---

## <a name="section-c"></a> 3. Percentages
```{python}
low = dist.cdf(177.8)    # 5'10"
high = dist.cdf(185.4)   # 6'1"
low, high
'''
Percentage of U.S male population that are at least 5'10" is 48.9%.
Percentage of U.S male population that are at least 6'1"  is 83.2%.
'''

```

---
