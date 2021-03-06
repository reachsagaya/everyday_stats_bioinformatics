# hamming_distance & normal distribution, equal variance
Ruijuan Li  
8/29/2017  

#### hamming distance

If both x and y are vectors, hamming.distance returns the Hamming distance (number of different elements) between this two vectors. If x is a matrix, the Hamming distances between the rows of x are computed and y is ignored.


```r
# install.packages("e1071")
library(e1071)
```

```
## Warning: package 'e1071' was built under R version 3.2.5
```

```r
x <- c(1, 0, 0)
y <- c(1, 0, 1)
hamming.distance(x, y) 
```

```
## [1] 1
```

```r
z <- rbind(x,y)
z
```

```
##   [,1] [,2] [,3]
## x    1    0    0
## y    1    0    1
```

```r
rownames(z) <- c("Fred", "Tom")
hamming.distance(z)
```

```
##      Fred Tom
## Fred    0   1
## Tom     1   0
```

```r
hamming.distance(1:4, 4:1) 
```

```
## [1] 4
```

We always have concerns that our data is not normally distributed, and/or should we transform the data to make it more nomrally distributed for analysis? So I did a bunch of google search to seek the answer. 

Here is a discussion on when to use parametric (with assumption of data distribution, usually normal distribution) and non-parametric method (no assumption on data distribution) for data analysis. 

This post described when the sample size is too small and median is a better representation of the whole data, it is better to use non-parametric method, otherwise, parametric method is preferred even on non-normally distributed data 

http://blog.minitab.com/blog/adventures-in-statistics-2/choosing-between-a-nonparametric-test-and-a-parametric-test

Here is another discussion on how normal distribution affect the method to choose for data analsys. 
https://www.sheffield.ac.uk/polopoly_fs/1.579191!/file/stcp-karadimitriou-normalR.pdf

another one 

http://blog.minitab.com/blog/quality-business/common-assumptions-about-data-part-2-normality-and-equal-variance

and another one 

http://www.unm.edu/~marcusj/testingassumptions.pdf

#### My understanding: 

after checking my notebook, equal variance is the most important for ANOVA, because it is a test called "analysis of variance". I remembered that during class, the instructor showed that using T-test and ANOVA test on data with unequal variance gave different result, where ANOVA says significantly different but T-test does not. Normal distribution is also important but less than equal variance.

After getting a data, the first thing to check is normal distribution and equal variance. Normal distribution can be checked by normal test or histogram, normality test is more stringent, if the data is roughly normally distributed, it should be fine to use ANOVA or other parametric method, which have a assumption of the data distribution and variance. Otherwise, the equivalent of non parametric method can be used, but non parametric method also has its own requirement, which is stated in the first linked post of this file. 

More to explored... 



