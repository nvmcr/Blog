<details>
<summary>Table of Contents</summary>

## Table of contents
Please use the github's interactive navigation. (Too lazy to write/generate TOC)

![toc](../Machine_Learning/Images/toc.gif)

</details>

# Intro
## Random Sampling and Sample Bias
A sample is a subset of data from a larger data set called population. 
> Random Sampling is a process in which each member in population has equal chance of being chosen for sample.

If sampling is not random, it will result in sample bias i.e the sample does not represent the population.

> Descriptive statisics are used to summarize and describe the characteristics of a dataset. Measures like mean, median, and standard deviation are examples of descriptive statistics.
>  Inferential statistics are used to draw conclusions about a population based on a sample of data. Techniques like hypothesis testing and confidence intervals are examples of inferential statistics.

Data distribution is the frequency distribution of **individual values** in a data set. Sampling distribution is the frequency distribution of **sample statistic**(mean, median etc) over many samples. People deal with samples beacuase dealing with millions of large populations is not practically ideal.
## Limit Theorems
### Sample Mean
Let $X_1$,.. $X_n$ be a sequence of iid random variables. The sample mean is given by

$$ S_n = {1\\over n}{\sum_{i=1}^n X_i} $$
### Weak Law of Large Numbers
$$ \lim_{n\to\infty} P(|S_n-\mu|>k)=0 $$

As the sample size n approaches infinity, the sample mean **converges in probability** to the true population mean. This means that as the sample size gets larger and larger, the probability that the sample mean deviates from the true population mean by more than k approaches zero.
### Strong Law of Large Numbers
$$ P(\lim_{n\to\infty} S_n = \mu) = 1 $$

As sample size n approaches infinity, the sample mean **converges almost surely** to mean. This provides a theoretical justification for the use of sample means as unbiased estimators of population means.

For example, a coin might land on heads 5 times in a row, but over a much larger n we would expect the proportion of heads to be approximately half of the total flips. Similarly, a casino might experience a loss on any individual game, but over the long run should see a predictable profit over time.
### Central Limit Theorem
It states that if we repeatedly sample a random variable a large number of times, the distribution of the sample mean will approach a normal distribution regardless of the initial distribution of the random variable.

$$ S_n = {{X_1+X2+...X_n}\\over n} \sim N(\mu,{\sigma^2\\over n}) $$

In other terms,

$$ {(S_n - \mu)\\over {\sigma\\over \sqrt(n)}} \sim N(0,1) $$

# Probability Distributions
## Normal Distribution
The well-known bell curve.

$$ f(x) = \frac{1}{\sqrt{2\pi\sigma^2}} \ e^{-\frac{(x-\mu)^2}{2\sigma^2}} $$

* Mean, median and mode are exactly the same.
* Around 68%, 95% and 99.7% of values are within 1,2,3 standard deviations from the mean respectively.
### Z-Distribution/ Standard Normal
Normal distribution with mean 0 and standard deviation 1. We convert normal to standard normal to calculate confidence intervals, perform hypothesis tests etc. The **z-scores** tells us how many standard deviations away from mean each value lies. This is also called **standardization**

$$ z = {x-\mu}\\over \sigma $$

Each z-score is associated with a probability or **p-value** that tells us the likelihood of values below that z-score occurring. This is the area under the curve left or right of that z score.

![pvalue](pval.png)
### T-Distribution/ Student
The t-distribution is a type of normal distribution that is used for smaller sample sizes. It has heavier tails than the normal distribution. As a result, the t-distribution has more probability in the tails and less in the center than the normal distribution. The variance in a t-distribution is estimated based on the degrees of freedom(df) of the data set. A **t-score** is the number of standard deviations from the mean in a t-distribution.
> Degrees of freedom (df) is the number of independent pieces of information used to calculate a statistic. It’s calculated as the sample size minus the number of restrictions. In most cases, df = Sample Size - 1

As the degrees of freedom increases, the t-distribution will get closer and closer to matching the z-distribution, until they are almost identical (df>30).
### Standardization vs Normalization
Say we have a dataset with `Age` and `Salary` columns. Range of age is usually 0-100 but salary has a bigger range and values. Using them without any feature scaling technique will make salary dominant in distance based algorithms. Two main feature scaling technique are standardization and normalization.

Standardization transforms data to have a mean of zero and a standard deviation of one. It preserves the shape of the distribution of the original data, but it changes the scale and location of the data. So it is used when we know the underlying distribution and highly preferred over normalization as it is robust to outliers. Preferred where gradient descent is used for convergence.

Normalization is used to rescale data to a range of 0 to 1 or -1 to 1. Normalization is often used when the absolute values of the data are less important and we dont know the underlying distributions.

$$ x' = ({2*(x - min)\\over (max - min)}) - 1 $$

## Chi-Square ($X^2$) Distribution
It is a continuous probability distribution that arises in the context of hypothesis testing and confidence interval estimation for the variance of a normally distributed population. The shape of the distribution is determined by the parameter df, which represents the degrees of freedom. 

Imagine taking a random sample of a standard normal distribution (Z). If you squared all the values in the sample, you would have the chi-square distribution with df = 1. $Χ_2^1 = (Z)^2$

Now imagine taking samples from two standard normal distributions (Z1 and Z2). If each time you sampled a pair of values, you squared them and added them together, you would have the chi-square distribution with df = 2. $Χ_2^2 = (Z_1)^2 + (Z_2)^2$

More generally, if you sample from k independent standard normal distributions and then square and sum the values, you’ll produce a chi-square distribution with k degrees of freedom. 

$$ Χ_k^2 = (Z_1)^2 + (Z_2)^2 + … + (Z_k)^2 $$

* Mean and variance is k and 2k respectively.
* When df is 1 or 2, the distribution looks like 90degress clockwise rotated `J`.
* When df is greater than 2, the distribution is right-skewed normal distribution.
* When df is greater than 90, the distribution looks like normal distribution.
# Sample Statistics
A sample statistic is a numerical measure that summarizes the characteristics of a sample of data. It is calculated from the sample data and is used to estimate the corresponding population parameter. It could be mean, standard deviation, variance, median, mode etc. Sample statistics are subject to sampling variability, which means that different samples of the same size from the same population may produce different sample statistics. This is why we use histograms, boxplots, violin plots, standard errors, confidence intervals and hypothesis testing to quantify the uncertainty in our estimates and make statistical inferences.
## Standard Error
W.K.T standard deviation represents variability of individual data values (in a single sample. To get variability of sampling distribution (over multiple samples), we calculate **standard error**. For a standard deviation of s and sample size of n, SE is given by:

$$ SE = {s\\over \sqrt(n)} $$

## Confidence Intervals
We deal with two different types of data, normally distributed or proportions. Population proportion refers to the proportion or percentage of individuals in a population who have a particular characteristic of interest. For example, if we are interested in the proportion of people in a city who own a car, the population proportion ($p$) would be the percentage of all people in that city who own a car. But again estimating something from all population is not practical so we use sample proportions $\hat{p}$. We could take a random sample of 500 people from the city, and count how many of them own a car. Let's say we find that 300 people in the sample own a car. The sampling proportion is then 300/500 = 0.6, or 60%. This 0.6 also represents mean of proportion. Standard devaition is calculated by $\hat{p}(1-\hat{p})$

Though sampling proportions help with estimating the population proportions, how confident are we about samples? We might be different proportions with different samples. So we try to give a range of values instead of a single value called confidence interval.
> A confidence interval is a range of values that likely contains the true value of a population parameter with a certain degree/percentage of confidence.

In other words, it is the mean of your estimate plus and minus the variation in that estimate. This is the range of values we expect our estimate to fall between if we redo our test, within a certain level of confidence. The level/percentage of confidence tells us the percentage of times we expect to reproduce an estimate between the upper and lower bounds of the confidence interval set by $CL = 1 - \alpha$. If we use $\alpha$ of 0.005, we represent 95% confidence level.

To calculate confidence interval we need test statistics like Z-score, t-scores and sample statistics like mean.

$$ CI = \hat{X} \pm ((Z)^*(or)(t)^*){\sigma\\over \sqrt(n)} $$

In case of proportions,

$$ CI = \hat{p} \pm ((Z)^*(or)(t)^*)\sqrt{\hat{p}(1-\hat{p})\\over n} $$

# Hypothesis Testing
## Test Statistics

# References
The information is pulled from various sources from internet. Major sources are:
1. [Practical Statistics for Data Scientists](https://www.oreilly.com/library/view/practical-statistics-for/9781491952955/)
5. [Ace the Data Science Interview](https://www.acethedatascienceinterview.com/)
6. ChatGPT :)