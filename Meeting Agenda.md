**Table of Contents**

- [December 2018](#december-2018)
    + [12/05/2018](#12-05-2018)
      - [Topics discussed](#topics-discussed)
      - [Things to Do](#things-to-do)
      - [Plans for next meeting.](#plans-for-next-meeting)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>



## December 2018

#### 12/05/2018

##### Topics discussed

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
  pay = \frac{-(\alpha_0 + \alpha_1X)}{\alpha_2}
$$




  4) The effects from individual characteristics are all going to the numerator. So add the coefficients into the coefficients of wetlands, as the mean of the exponential distribution for wetlands. 





- The "Standard  Error", "95% CI" for the estimated coefficients itself, same as the variance-covariance matrix. So theoretically, from  Multivariate normal distribution, we should be able to do the simulation for all estimated coefficients.  --> the uncertainty from the sample :smiling_imp:
- By drawing the coefficients for each individual, we are catching the heterogeneity in the sample.  :alien:(should make a decision between the two.)



- About the coefficients of dummy variables in WTA simmulation. 

  - Farmarea_1, 2, 3, 4. 

    1)  farm size share at county level times each of the coefficients for each category, and then take an average 

  - Income_1, 2, 3, ..,7

    1) Find the income distribution for each county, and then do the similar stuff. 




#####  Things to Do

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



##### Plans for next meeting. 

- Simulation of WTA in R
- Uncertainty of WTA (discuss about the literature)
- EA epistasis 



#### 12/06/2018

##### Topics discussed

- Simulate WTA

  ```
  wta_largefarm_repubs <- -(-1.32104 - 0.0006*483 - 1.75395 * rexp(10000,1))/(0.00758*rexp(10000,1))
  ```

  - Note the coefficients of Wetland and Payment are "random distributions"

##### Things To Do

##### Plans for next meeting

