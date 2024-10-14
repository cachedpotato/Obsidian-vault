---
tags:
---
# Variance Stabilizing Transformation
Empirical measurements are different from theoretical replicates in that the replicates are in fact, not exactly the same. This means in an experimental setting, it's harder for us to know if the difference in observation is a true/significant difference between conditions or just biological noise. 

## Heteroskedasticity
Heteroskedasticity means the variance of errors is not constant across observations. In other words, the variance of our data is different in different regions of our data space. For example, the variance may increase along one axis with the mean.
![[heteroskedasticity1-1024x390.webp]]
This is troublesome for regression tasks, as regression normally assume _homoskedasticity_ - the variance remains the same through our data space.

To mitigate this problem, we need some sort of preprocessing to our data to make the variance consistent. This is called **variance stabilizing transformation**.

## Example VST
One common way of applying such transformation is to simply apply square root to the variables.

---
Categories: [[050-Statistics]], [[Bioinformatics]]
References:
https://corporatefinanceinstitute.com/resources/data-science/heteroskedasticity/
