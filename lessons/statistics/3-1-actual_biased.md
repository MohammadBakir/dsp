[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

---

## Problem Statement

Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.

Use the NSFG respondent variable NUMKDHH to construct the actual distribution for the number of children under 18 in the household.

Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.

Plot the actual and biased distributions, and compute their means. 

--

#### Steps to solve the problem
[1)  Import required libraries and packages](#section-a)  
[2)  Read data using nsfg.ReadFemPreg](#section-b)  
[3)  From Response Data Plot Probability Distribution of numkdhh](#section-c)  
[4)  Define BiasPmf and calculate BiasPmf](#section-d)  
[5)  Generate plot to show side by side comparison of pmf and biased pmf](#section-e)  
[6)   Calculate Means](#section-f)  

---

## <a name="section-a"></a> 1. Imports

```{python}
import nsfg
import thinkstats2
import thinkplot
```
---

## <a name="section-b"></a> 2. Read data
```{python}
resp = nsfg.ReadFemResp()
```
---

## <a name="section-c"></a> 3. Plot Probability Distribution
```{python}
pmf_household_children = thinkstats2.Pmf(resp.numkdhh, label='numkdhh')
thinkplot.Pmf(pmf_household_children)
thinkplot.Config(xlabel = 'Number of Children', ylabel = 'PMF')
```
![Image of PMF Plot](Images/PMF.png?raw=true)
---

## <a name="section-d"></a> 4.Bias Bmf
```{python}
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)
    
    for x, value in pmf.Items():
        new_pmf.Mult(x, x)
        new_pmf.Normalize()
        
    return new_pmf

biased_pmf = BiasPmf(pmf_household_children, label='biased')
```
---

## <a name="section-e"></a> 5. Side by Side Distribution Comparison
```{python}
thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf_household_children, biased_pmf])
thinkplot.Show(xlabel = 'class size', ylabel = 'PMF')
```

![Image of BiasedPMF Plot](Images/BiasedPMF.png?raw=true)
---

## <a name="section-f"></a> 6. PMF VS Bias Means
```{python}
pmf_household_mean = pmf_household_children.Mean()

biased_pmf_mean = biased_pmf.Mean()


print (pmf_household_mean, biased_pmf_mean)
```
