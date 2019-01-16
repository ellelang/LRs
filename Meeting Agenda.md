**Table of Contents**

[TOC]





## December 2018

### 12/05/2018

#### Topics discussed

- DCM results from NLOGIT6. 

  + by setting the **exponential distributions** for Wetlands, cover crop, nutrient management, and payment, all coefficients are significant. 
  + Procedure of recovering the WTA for wetlands:

  1) take the estimated wetland coefficient  (i.e. the mean ) to generate the random number with Exponential distribution.

  2) take the  estimated payment coefficient  (i.e. the mean) to generate the random number with Exponential distribution.

  3) use the ratio of exponential distribution samples to get the samples of WTA_wetlands

   --> or take a look at the CDF of exponential ratio https://math.stackexchange.com/questions/33778/cdf-of-a-ratio-of-exponential-variables

  - WTA can always be estimated by the ratio of two   coefficients


$$
U(vp) = \alpha_0 + \alpha_1X + \alpha_2pay \\
  
  U(current) = 0 \\
  
  U(vp) = U(current) \Rightarrow \\
  \alpha_0 + \alpha_1X + \alpha_2pay = 0 \Rightarrow \\
  pay = \frac{-(\alpha_0 + \alpha_1X)}{\alpha_2}
$$




  4) The effects from individual characteristics are all going to the numerator. 

- The "Standard  Error", "95% CI" for the estimated coefficients itself, same as the variance-covariance matrix. So theoretically, from  Multivariate normal distribution, we should be able to do the simulation for all estimated coefficients.  --> the uncertainty from the sample :smiling_imp:
- By drawing the coefficients for each individual, we are catching the heterogeneity in the sample.  :alien:(should make a decision between the two.)



- About the coefficients of dummy variables in WTA simmulation. 

  - Farmarea_1, 2, 3, 4. 

    1)  farm size share at county level times each of the coefficients for each category, and then take an average 

  - Income_1, 2, 3, ..,7

    1) Find the income distribution for each county, and then do the similar stuff. 

#### Things to Do

- Stuff To Read

> A. Applied Choice Analysis : A primer (for the Nlogit directory setting)
>
> B. Valuing environmental and natural resource pp.107   (4. 3 The dispersion of Willingness to Pay)
>
> C. A Combinatorial Optimization Approach to Nonmarket Environmental Benefit Aggregation via Simulated Populations
>
> D. Using Geographically Weighted Choice Models to Account for the Spatial Heterogeneity of Preferences
>
> E.  Green subsidies in agriculture: Estimating the adoption costs of conservation tillage from observed behavior
>
> F. On finite sample performance of confidence intervals methods for willingness to pay measures
>
> **EA. Epistasis** (The papers mentioned in last Friday's meeting)
>
> 2A. Water Routing theory
>
> 2B. Optimal Spatial Management of Agricultural Pollution
>
> 2C. MULTIPLE CRITERIA DYNAMIC SPATIAL OPTIMIZATION TO MANAGE WATER QUALITY ON AWATERSHED SCALE

#### Plans for next meeting. 

- Simulation of WTA in R
- Uncertainty of WTA (discuss about the literature)
- EA epistasis 



###  12/06/2018

#### Topics discussed

- Simulate WTA

  ```
  wta_largefarm_repubs <- -(-1.32104 - 0.0006*483 - 1.75395 * rexp(n = 10000,rate = 1))/(0.00758*rexp(n = 10000,rate = 1))
  ```

  - Note the coefficients of Wetland and Payment are "random distributions"

  - The expected WTA of wetland for land owner i at county j 
    $$
    E(WTA_{ij})_{wetland} = E[\frac{\beta_{asc}\cdot 1 + \beta_{wetland}\cdot \text{RandomDraws} + \beta_{cc}\cdot 0 + \beta_{nm}\cdot 0 + \beta_{dem18}\cdot dem18_j + \beta_{tax} \cdot tax_j + \sum^6_{k=1}\beta_{income} \cdot income_{ij} + \sum^4_{k=1}\beta_{area} \cdot areaf_{i}}{\beta_{pay}\cdot \text{RandomDraws}}]\\
    
     
    $$




    The random draws are from exponential distribution based on the assumptions about the random parameters
    $$
    \beta_{wetland}, \beta_{pay},\beta_{cc},\beta_{nm} \sim rexp(n, rate = 1)
    $$


    How to apply the WTA got from survey sample to the candidate sites of WCMO?
    
    - farm size can be got from the cluster area information in  .shapefile
    - farm income: can use the average income of specific farm size as an indicator (see the size/income table  <https://finbin.umn.edu/FmSummOpts/Index>)

#### Things To Do

- 

Plans for next meeting



## January 2019

### 1/11/2019

#### Things to Do

1. Simulate WTA 
   $$
   E(WTA|X) = \frac{\sum \beta_k}{\beta_p} = \frac{U(V) - pay\times Payment}{\beta_p}
   $$

2. General Exam Prep
   - [ ] list the papers you prepare for your Thesis
   - [ ] proposal is the combination of the "Abstracts" of these papers
   - [ ] Show the committee that you know what you are doing / you have solid understanding about the topic
   - [ ] Then seek for advice from the committee
   - [ ] The practical implement of your project & public media--> write a scientific blog 
   - [ ] send out the draft and slides before the meeting. 



### 1/14/2019

1. WTA simulation - three sources of uncertainties. 

   There are three sources of randomness or variation in a willingness to pay measure: 

   - randomness of preferences ("Taste heterogeneity", uncertainties from individual observation )

   - randomness of estimated parameters (maximum likelihood distributions. e.g.  K-B process: draw new vector of parameters from the multinomial distribution 

     ```R
     rmvnorm(mean = beta_est, sigma = vcov(beta_est)) ) 
     ```

   - variation across individuals in the sample. 
     $$
     \bar{E(WTP_i)} = \frac{\sum^T_{i = 1}g(z_i|\beta)}{T}
     $$
     The interpretation of this quantity is the sample average expected WTP with respect to random preferences. That is, it is the sample average value of the measure of WT P found by taking the expectation of WTP with respect to individual randomness. 

2. Procedures for DCM project:

​       Goal: want to get the individual WTA respected to individual location (WTA|X), where X includes the characteristics for the sample.

- [ ] get the parameter estimates from RPL. For wetland, payment, cc, nm, are the means of exponential  distributions. 

- [ ] take the random draws from the exponential distributions (refer to the nlogit 6 manual--> how to recover the distributions assumption for exponential distribution)  eg. 

  ```
  betaest_wld <- beta_wld * rexp (rate = 1, n = 10000)
  betaest_pay <- beta_wld * rexp (rate = 1, n = 10000)
  ```

- [ ] add the effects from the fixed parameters to the est_wld.

- [ ] Calculate the ratio 
  $$
  WTA_i = \frac{\beta_{estwld} + Z_i\beta_i}{\beta_{pay}}
  $$

- [ ] Get the statistical parameters for WTA_i

  In the example above, we should have a WTA vector with10000 elements for each individual i. We can have the mean, median, and the 25%, 75% CI for the vector.  





2. Methods to build WTP CI

- Approximation 
  - Delta Method : produces symmetric CIs around WTP point estimates.  
- Bootstrap (simulation): Bootstrap methods use the simulated distribution of parameter estimates in place of their analytical one. These methods are computationally intensive and affected by Monte Carlo error
  - Different sampling strategies, either parametric or non-parametric, can be used to produce a bootstrap sample and, thus, a simulated WTP distribution



- Non-parametric resampling: 

  a). 1.  resample the observations w with replacement to generate a new sample; let this sample  have the same number of observations as the original one;

  b). fit the logit model to the bootstrap sample to obtain $\hat{\beta^*_b}$ and $\hat{WTP^*}$ 

$$
\hat{\beta^*_b} = (\hat{X}'\hat{X})^{-1}\hat{X}\hat{Y}
$$

- Krinsky and Robb resampling 

​        a). draw a vector $\hat{\beta^*_b}$ from the multinomial distribution 

```
rmvnorm(mean = beta_est, sigma = vcov(beta_est)) ) 
```

​       b) Use the vector  $\hat{\beta^*_b}$  to calculate $\hat{WTP^**}$
$$
<Empty \space Math \space Block>
$$

### 