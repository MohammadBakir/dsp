[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

---

#### Steps to solve the problem
[1)  Import required libraries and packages](#section-a)  
[2)  Read data using nsfg.ReadFemPreg](#section-b)  
[3)  From pregnancy data, extract live birth data](#section-c)  
[4)  From live birth data split data into those born first and those born after](#section-d)  
[5)  Compare Averages of total weight of those born first and the others](#section-e)  
[6)  Define Cohen Effect Size](#section-f)  
[7)  Calculate Cohen Effect Size](#section-g)  
[8)  Compare averages of length of pregnancies of those born first to others born](#section-h)  

---

## <a name="section-a"></a> 1. Import Required Libraries and Packages

import nsfg
import pandas as pd
import numpy as np
import thinkstats2

---

## <a name="section-a"></a> 2. Read data
preg = nsfg.ReadFemPreg()

--

## <a name="section-a"></a> 3. From pregnancy data, extract live birth data
live_births = preg[preg.prgoutcome == 1]

--

## <a name="section-a"></a> 4. From live birth data split data into those born first and those born after
first_born = live_births[live_births.birthord == 1]
others_born = live_births[live_births.birthord != 1]

--

## <a name="section-a"></a> 5. Compare Averages of total weight of those born first and the others
first_born_mean = first_born['totalwgt_lb'].mean()
others_born_mean = others_born['totalwgt_lb'].mean()

print(first_born_mean, others_born_mean)

'''
first_born_mean = 7.201094430437772
others_born_mean = 7.325855614973262
difference is negligible, per the mean first babies born are lighter than than others. 
'''

---

## <a name="section-a"></a> 6. Define Cohen Effect Size
'''
This functon computes the Cohen effect size, which is the difference in means expressed in number of standard deviations:
'''
def CohenEffectSize(group1, group2):
    """Computes Cohen's effect size for two groups.
    
    group1: Series or DataFrame
    group2: Series or DataFrame
    
    returns: float if the arguments are Series;
             Series if the arguments are DataFrames
    """
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
    return d
    
---

## <a name="section-a"></a> 7. Define Cohen Effect Size
CohenEffectSize(first_born.totalwgt_lb, others_born.totalwgt_lb)
'''
Cohen Effect Size  = -0.088672927072602
The size of the difference between the first born and others born is non significant. 
'''

---

## <a name="section-a"></a> 8. Compare averages of length of pregnancies of those born first to others born
first_born_prglngth_mean = first_born.prglngth.mean()
others_born_prglngth_mean = others_born.prglngth.mean()
print(first_born_prglngth_mean, others_born_prglngth_mean)

'''
Average Pregnancy Length of those born first is 38.60095173351461 
Average Pregnancy Length of those born second is 38.52291446673706
'''

#CohenEffectSize(first_born.prglngth, others_born.prglngth)
'''
Cohen Effect Size  = 0.028879044654449883
The size of the difference between the pregnancy length of those born first and the others is non significant. 
'''

---
