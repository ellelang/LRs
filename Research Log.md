**Table of Contents**





## December 2018

### 12/06/2018

#### Estimate WTA 

- The non-parametric bootstrap

  - resample the observations w with replacement to generate a new sample; let this sample  have the same number of observations as the original one;

  - fit the logit model to the bootstrap sample to obtain $\hat{\beta^*_b} and \hat{WTP^*}$

  1. ? sample the data w/ replacement to get (x^* and y^\*) , but how to get \beta^*? 

  2. ? Does non-parametric mean no specific function , e.g. MNL OR RPL for estimating \beta^*? 

- The parametric bootstrap

  - Let \beta^ be the MLE of obtained by fitting the logit model (e.g.  RPL) to the original data. 
  - Generate the random error \theta^* from a specific distribution, e.g. Gumbel)
  - Compute 

  $$
  \hat{U}^*_{int(b)} = X_{int}\hat{\beta} + e^*_{int(b)} \Rightarrow
  $$


$$
\hat{U}^*_{int(b)} > 0, \hat{y}^*_{int} = 1; otherwise,\ \hat{y}^*_{int} = 1
$$

1. These give the parametric bootstrap sample:

$$
(X, \hat{Y}^*_b)
$$

2. Then, use this bootstrap sample to estimate the  regression coefficient (e.g from RPL model) : 

$$
\hat{\beta}^*_b 
$$

3. ? Does this mean we need to involved the NLogit estimates for each round? Yes



- Krinsky and Robb resampling 

  - Draw bootstrap estimates from the  multivariate  normal  distribution. 

  $$
  \hat{\beta}^* \sim N (\hat{\beta}, \hat{\Sigma}_{\hat{\beta}})
  $$

  - Use the bootstrap beta to calculate bootstrap WTP

1. How to import the variance-covariance matrix to R quickly? (you don' t want to type them into R)

2. How to draw estimates based on variance covariance matrix? https://stats.stackexchange.com/questions/91682/how-to-draw-estimates-based-on-variance-covariance-matrix

   ​    a) 

```
p = 3 # number of parameters
newbeta <- coef(fit) + chol(vcov(fit))%*%rnorm(p)
newbeta
                   [,1]
(Intercept)  3.52525853
x1          -0.05357471
x2           0.11368681
```

OR.  b) Use the R function  rmvnorm(#,  mean=, sigma=) 



#### Miscellaneous

```
cat(paste(shQuote(var_names, type="cmd"), collapse=", "))
cat(paste(var_names, collapse=", "))
```

