**Table of Content** 

- [December 2018](#december-2018)
  * [12/03/2018](#12-03-2018)
    + [Multinomial Logit Models with Continuous and Discrete Individual Heterogeneity in R: The gmnl Package](#multinomial-logit-models-with-continuous-and-discrete-individual-heterogeneity-in-r--the-gmnl-package)
  * [12/04/2018](#12-04-2018)

############################

## Literature Review Rounds

#### 1st  PASS

1) Read the title, abstract & introduction. 

2) Read the sub-headings. 

3) Read the conclusion. 

4) Skim the references for familiar ones.

- Main topic: 
- Key Points: 
- Key Concept Definitions: 
- Contributions:



#### 2nd PASS (1 HOUR)

1) What does it do? 

2) How does it do it?

3) What did it find?



- Rationale
- Aims
- Hypothesis



- Methods



- Finds
- Implications:
- Falsifiable:
- Limitations:



#### 3rd PASS (2+ HOUR)

1) Strengths

2) Weakness



- Presentation Techniques:  
- Support for Conclusion:  
- Internal Efficacy:



- Pinpoint 
- Implicit Assumptions:  
- Experimental/Analytical Errors: 
- Missing Citations:







## December 2018



### 12/03/2018

#### Multinomial Logit Models with Continuous and Discrete Individual Heterogeneity in R: The gmnl Package



#### Points Collection

-  In all these areas the most widely used method to model choice among mutually exclusive alternatives has been the **Conditional or Multinomial Logit model (MNL)** ( McFad-den 1974 ), which belongs to the family of Random Utility Maximization (RUM) models.  

-  The most popular MNL extension is the Mixed Logit Model (MIXL). MIXL allows parameters to vary randomly over individuals by assuming some continuous heterogeneity distribution a priori while keeping the MNL assumption that the error term is independent and identically distributed (i.i.d) extreme value type 1.

  - using  the  parametric  heterogeneity distribution  that  describes  how  preferences  vary  in  the  population  it  is  possible  to  derive conditional estimates of the parameters at the individual-level
  - 



### 12/04/2018 

#### Are consumers willing to pay to let cars drive for them? 





### 12/05/2018

- Independence from Irrelevant Alternatives (or IIA), which is a result of the i.i.d. disturbances. The IIA property states  that, for a given individual, the ratio of the choice  probabilities of any two alternatives is unaffected by other alternatives. This  property was first stated by Luce (1959) as the foundation for his probabilistic choice model, and was a catalyst for McFadden’s development of the tractable multinomial logit model. There are some key advantages to IIA, for example , the ability to estimate a choice model using a sample of alternatives, developed by McFadden (1978). However, as Debreu (1960) pointed out, IIA also has the distinct disadvantage that the model will perform poorly when there are some alternatives that are very  similar to others (for example, the now famous red bus – blue bus problem).
-  MNL, NL, and CNL are all members of the General Extreme Value, or GEV, class of models, developed by McFadden (1978, 1981), a general and elegant model in which the choice probabilities still have tractable logit form but do not necessarily hold to the IIA condition. There is also the heteroscedastic extreme value logit model, which allows the variance of the disturbance to vary across alternatives. 

- Probit is extremely flexible, because it allows for an unrestricted covariance matrix, but is  less popular than the GEV forms primarily due to the difficulty in estimation  

- Logit kernel (or continuous mixed logit model) is a model that attempts to combine the relative advantages of probit and GEV forms. The disturbance of the logit kernel model is composed of two parts: a probit-like term, which allows for flexibility, and an i.i.d. Gumbel (or GEV) term, which aids in estimation.  There have been numerous relatively recent applications and investigations into the model (see Chapter 3). A particularly important contribution is McFadden and Train’s (2000) paper on mixed logit, which both (i) proves that any well-behaved RUM-consistent behavior can be represented as closely as desired with a mixed logit specification and (ii)  presents easy to implement specification tests for these models.
- Choice Process Heterogeneity. A key area of enhancements to discrete choice models is related to the idea that t here is heterogeneity in behavior across individuals, and ignoring this heterogeneity can result in forecasting errors. For example, Ben-Akiva, Bolduc, and Bradley (1994) demonstrated the significance of unobserved heterogeneity on the demand curve for toll facilities. The most straightforward way to address this issue is to capture so-called “observed heterogeneity” by introducing socio-economic and demographic characteristics in the systematic portion of the utility function (i.e., in ()Vg ). 
- The objective of this research is to develop a generalized discrete choice model to guide  the progress of models towards more behaviorally realistic representations with improved explanatory power. The resulting framework must be mathematically tractable, empirically verifiable, theoretically grounded, and have the ability to incorporate key aspects of the behavioral decision making process.  





### 12/06/2018



There are three sources of randomness or variation in a willingness to pay measure: 

- randomness of preferences, 
- randomness of estimated parameters and 
- variation across individuals in the sample.

Methods to build WTP CI

- Approximation 

  - Delta Method : produces symmetric CIs around WTP point estimates.  

- Bootstrap (simulation): Bootstrap methods use the simulated distribution of parameter estimates in place of their analytical one. These methods are computationally intensive and affected by Monte Carlo error

  -   Different sampling strategies, either parametric or non-parametric, can be used to produce a bootstrap sample and, thus, a simulated WTP distribution



- Non-parametric resampling: 

  a). 1.  resample the observations w with replacement to generate a new sample; let this sample  have the same number of observations as the original one;

  b). fit the logit model to the bootstrap sample to obtain $\hat{\beta^*_b} and \hat{WTP^*}$
$$
\hat{\beta^*_b} = (\hat{X}'\hat{X})^{-1}\hat{X}\hat{Y}
$$

- Krinsky and Robb resampling 

​                      a). draw a vector \hat{\beta^*_b} 

​                      b) Use the vector  \hat{\beta^*_b}  to calculate \hat{WTP^*}