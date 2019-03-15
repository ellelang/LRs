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

### 1/16/2019 

- Delta Method: essentially is the application of The Taylor Expansion
- KR method for lognormal distribution: 

$$
\beta_i = \hat{\beta_k} + Cz_k = \bar{\beta} + \hat{\sigma} x_k + Cz_k\\ 

\Beta = exp(\bar{\beta} + \hat{\sigma} x_k + Cz_k)
$$

where x_k and z_k are  independent standard normal random variables. 

C is the lower Cholesky decomposition matrix. 

Nlogit 6  P563. 

Nlogit 6 can do the delta method simulation



- The paper https://www.mendeley.com/catalogue/confidence-intervals-willingnesstopay-random-coefficient-logit-models/

do a good job explaining the ins and outs of uncertainty in RPL models. They also provide Delta method formulas but for an exponential, the K&R loop is pretty easy (beta_draw = betahat*rexp(1) + C*z)...

Doing draws based on exponential distribution alone helps characterize the extent of preference heterogeneity, but if you want confidence intervals, it's either KR or Delta method.

- Loop over r we get the same draw from multivariate normal, but this snippet seems to show that we get a different draw every time (which is what we want)

```R
##########cc wta
draws <- matrix (NA,nrow = R, ncol = 19)
colnames(draws)<-c('wetland','pay','cc','nm','asc','dems18','costtax',
                   'inc1','inc2','inc3','inc4','inc5','inc6',
                   'farm1','farm2','farm3','farm4','crp','cclake')

  for (r1 in 1 : R){
    drawbetas<- betas
    drawbetas$Betas <- as.vector(rmvnorm(1,mean = betas$Betas, sigma = varcov_m))
    draws[r1, ] <- drawbetas$Betas
  }

  for (r in 1 : R){
    newbetas <- draws[r,]
    pay_rp <- newbetas["pay"]
    cc_rp <- newbetas["cc"]
    lake_rp <- newbetas["cclake"]
  }
```



- The parameters for observable heterogeneity should not be called "fixed parameters". They are individual specific parameters. In the Nlogit6 output, the name "fixed" means the means of these random parameters are fixed.   
- How you might use the uncertainty of WTA at a specific location to say something about practices/locations which may be robust to cost assumptions?



## March 2019

### 3/6/2019

Dear Committee,

Thank you so much for allowing me to pass the general exam and giving me the opportunity to continue my study in the Ph.D. program! That really means a lot to me!! 

I appreciate your precious time and invaluable feedback for my research proposal! In the next stage, I will follow the logic in the proposal to write up my thesis. Following your suggestions, I will dig deeper into the landowner survey data, learn more about the ecosystem services valuation,  and study the dynamic changes and conservation timeline issues!  The suggestions and feedback from all of you are treasures for me, so if you have any advice at any time, please let me know!

Trevor, I hope you will get better soon!!

Thank you so much again!



### 3/14/2019



#### Things to do

- [ ] MOSM paper discuss about the "net cost" in the "Discussion"

  - Essentially is related to "Water quality evaluation"

  - Net cost = Cost - monetary value of the environmental benefits
  - Under the assumption that the marginal benefits keeps the same (not true though): for duck hatchlings: $2.5/hatchlings * number of hatchlings will be the monetary values; and similar with the sediment reduction
  - The shortcomings of using the "monetary values" about the benefits: ignore the co-benefits of the conservation actions (such as the positive effects on nitrogen reduction, stream health, and other wildlife... )

- [ ] Comment on the MOSM paper methodology part

  - The new parts that Sergey added 

- [ ] Epistasis computational experiment

  - Construct the argument framework to justify the methodology
    - EAs work quite well in the context of water quality research
    - Epistasis doesn't have significant effects when the size of the decision variables is small
    - The scale of the problem matters
    - Therefore, when will epistasis be a problem?

  - Use the synthetic test problems that have known solutions to do computational experiments

    - Read papers shared by Sergey to find the proper synthetic problems

    - Identify different form of epistasis
    - Exam the degree of epistasis --> when BCR works well, and when it fails!

  - Why we use SPEA2 ? 
    - Response to the critiques from WRR
    - Use Python deap?



#### The letters from WRR Reviewers:

 (https://mail.google.com/mail/u/1/#search/WRR+paper/FMfcgxvzLhklvQnhbspkXWjVRkKNLNnB)

Dear Dr. Rabotyagov: 

Thank you for submitting your manuscript to Water Resources Research. I have received the Associate Editor's assessment based on three reviews of your manuscript. 

I am sorry to inform you that based on the reviews of your manuscript, I have decided to decline it for publication in Water Resources Research at this time. While the reviewer's comments range from minor revisions to major revisions, the AE has a number of concerns that will take substantial amount of time and effort to address. As such, I believe that it is best to decline your paper now, so as not to put a time constraint on your revision and allow you ample time to complete the additional work.

While the manuscript is not acceptable now, with additional work, as outlined in the comments, it is possible that you will be able to turn this into a more suitable paper. You are welcome to resubmit your paper to WRRonce you address the concerns raised in the review process.

-----

If you resubmit this paper, please follow our Checklist and use our Templates for the main file and any supplements. Please provide the following: 

1. A response to reviewer file that lists each major comment and describes how the manuscript has/has not been modified. 

2. A copy of the manuscript with the changes noted (e.g., highlighted, "track changes," italics or bold changes). 

3. The final revised manuscript and separate final figure and supporting information files with the changes incorporated, which will be used for publication if the manuscript is accepted.

AGU requires that data needed to understand and build upon the published research be available in public repositories following best practices. This includes an explicit statement in the Acknowledgments section on where users can access or find the data for this paper. Citations to archived data should be included in your reference list and all references, including those cited in the supplement, should be included in the main reference list. All listed references must be available to the general reader by the time of acceptance. AGU requires the corresponding author, and encourages all authors, to register for an ORCID.

When you are ready to submit your revision, please login to your account (https://wrr-submit.agu.org/cgi-bin/main.plex) and click "Revise 2018WR024012." 

I look forward to receiving your revised manuscript. If you have any questions, please contact us at wrr@agu.org.



Yours sincerely, 

Martyn Clark
Editor-in-Chief
Water Resources Research 

------------IMPORTANT INFORMATION------------------------ 
Additional information on text preparation, formatting, acceptable file formats, supporting information, graphics preparation, and AGU style, is here. AGU has recently updated its styles. 

Sharing your work is an important part of the research process, and AGU leverages and shares published research to promote the https://eos.org/editors-vox/earth-and-space-science-for-the-benefit-of-humanity" target="_blank">broader importance of Earth and space science. Learn how you can promote your paper, including how your paper can be considered for additional publicity or for the issue cover.

------------------------------------------------------------------------------
Associate Editor Evaluations:

Associate Editor (Remarks to Author):

The manuscript entitled "Good Seeds Bear Good Fruit: Using Benefit-to-cost Ratios in Multiobjective Spatial Optimization under Epistasis" presents an application of the SPEA2 algorithm in spatial land management decisions in a multiobjective framework. The paper has received 3 reviews ranging from Minor Revisions to Major Revisions. Although Reviewer #1 says Minor Revision, their detailed comments do in fact request a more careful verification of the proposed search results. At the core of this contribution is the challenge of a very large binary decision space (10,000 binary decision variables) that have spatial linkages (or epistatic dependencies) causing the problem to potentially be very difficult. The premise of the work is to use a dimensionally aggregated cost-benefit version of the problem to inform subsequent search efforts. There are three core issues in the search problem (1) selection and variational operators struggle to respect dependencies across landscape decisions; (2) temporal salience structure in the sense that the different decision variables will have marginally less impacts on distinguishing objective space performance leading to genetic drift stall (i.e., can you show all decision variables converge even in the aggregate case?); and (3) the stability of search subject to preconditioning with a subspace variant of the problem. The algorithm employed is strongly dated relative to the state-of-the-art and it is not clear why the authors are using a binary representation. Their justifications are self-citations to their prior papers. The landscape decisions could have been discretized in a myriad of ways to reduce the original problem's dimensionality. Representation changes could include zonation methods, embedded universal approximators for feature mapping, or even network topological abstractions. I would encourage the authors to explore spatial optimization in the broader evolutionary computation literature. Overall, I have strong reservations related to generality and adequacy of the proposed work. The revised manuscript should address the following major concerns raised by the reviewers: (1) clarify the specific scientific and institutional context of the problem being presented in terms of how it relates to real world land rights and decisions processes; (2) clarify and better substantiate the core technical contributions of the work as a generalizable framework; (3) better contextualize and justify the use of a relatively dated solution algorithm; (4) carefully benchmark the search dynamics of the algorithm relative to an equivalent random baseline (i.e., would a very large random Monte Carlo sample of the size equivalent to the number function evaluations used per seed trial of SPEA2 yield fully dominated solutions? can you prove that the resulting decision variables have converged to values that are not simply an artifact of a very large random sample?); and (5) provide formal statistical metric-based evaluations of search dynamics for multiple seeds to verify the value of the preconditioning relative to the full problem.

The challenge in this work is that the Pareto efficient frontier should in theory be extraordinarily difficult to approximate so this creates the danger of false sense of performance. There could be reasons why the problem is not as difficult as it appears for example the decision variables are largely redundant, lack impact, and are non-unique in yielding Pareto approximate performance (i.e., equifinality as noted by Reviewer #1).

Overall, the theory of evolutionary heuristics does not strongly support that the claimed insights of the authors are more than artifacts of large random sampling. Given the immense complexity of the mathematical space, the authors need to better support their results with clear empiric search baselines and metrics. Perhaps more importantly, the authors need to be sure that the representation of the problem has real world decision relevance.

Overall I believe the authors should be given the opportunity to contemplate a Major Revision. In my own assessment of the work, although well written the current claimed results are questionable and should be Rejected unless clearly substantiated.


Reviewer #1 Evaluations:
Significant (Required): Yes, the paper is a significant contribution and worthy of prompt publication.
Supported (Required): Yes
Referencing (Required): Yes
Quality (Required): Yes, it is well-written, logically organized, and the figures and tables are appropriate.
Data (Required): Yes
Accurate Key Points (Required): Yes

Reviewer #1 (Formal Review for Authors (shown to authors)):

Review of Lang et al., WRR 2018

This paper considers multi-objective optimization with spatially distributed decision variables, using the example of land management in a watershed. This leads to the specific problem of epistasis, or nonlinear interaction between the decision variables, which traditionally causes problems for heuristic solution techniques including evolutionary algorithms. The authors design a clever experiment to quantify the extent of epistasis in an example problem, and develop a strategy using a separability assumption to generate initial solutions for the MOEA that lead to improved performance. 

The paper is exceptionally well-written, and the presentation is clear and concise. The research question has some theoretical precedent in other journals, but it is a novel contribution to introduce and quantify the issue of epistasis with a focus on spatial optimization, which will be accessible for the WRR readership. I have only a few clarifying questions that likely fall somewhere between a minor and major revision.

1. The large size of the search space must make convergence difficult. If I understand table 3 correctly, there are on the order of 10,000 binary decision variables, suggesting a search space of 2^10000 possible combinations of management options.

I am surprised that the unseeded MOEA run (resulting in Pareto front F0) is able to find decent solutions, given this difficult search space. Especially since Table 4 indicates on the order of 16,000 generations (w/population size 16) to converge. I would suggest that the authors include plots of the MOEA convergence vs. function evaluations, perhaps as supplemental material, to better understand this outcome.

The metric used to confirm convergence is reasonable, and of course with a MOEA we aim only for approximately-optimal solutions. I suggest this exploration only because the result is surprising given the apparent difficulty of the problem.

2. A related question given the size of the search space, is there any concern about equifinality in the decision variables? Many different combinations of decision variables could result in approximately similar performance, and this warrants more discussion.

For example, one important finding is that 90% of the initial solutions based on the BCR remain nondominated in the final set. First, to confirm: is this 90% value determined based on a matching between the binary decision variables? Second, does this confirm that they are part of the Pareto front, or only that no improving mutation was found during the limited search time ? (216 generations, per Table 4)

3. Section 2.3 describes how the benefit-cost ratio (BCR) is used to determine solutions to the linearized version of the problem. This could be clarified. The variable lambda is clear, as this aligns with a typical weighting approach to multi-objective problems. However, the variable k warrants more explanation. How is this chosen? This seems like an important second degree of freedom to create the BCR solutions.

4. Finally, I have some concern about the generalizability of the paper, for two reasons. First, the findings depend on the degree of epistasis in the problem considered. This case study only has one epistatic objective function (the other two are linear and separable). The authors do quantify the degree of epistasis, which is a nice contribution. But I still wonder if the same approach would work in a different system where the difference between the separable and non-separable problems is larger.

Second concern about generalizability: in this case study, the benefits of individual management options are assumed to be known. Would this information be available in general for another system? And if not, would that hinder the use of this method to generate initial solutions?

Minor comments

- The experiment does not include multiple random seed trials, which would be standard for an MOEA experiment. The authors should justify this choice. 

- A related point, the use of the word "seed" throughout the paper may be confusing, because it typically refers to random seeds for EA studies, when really the authors are referring to initial solutions given to the EA.

- The title could be more clear than "using" benefit-cost ratios, maybe including something about initial solutions.

- The figure legends throughout the paper should use clear names instead of the abbreviations that are not explained in the text. (Fig 2 for example)

- Around line 465 it is suggested that scaling ratios can be determined that essentially convert the nonlinear (epistatic) problem into a separable one. Would that allow the problem to be solved as a regular knapsack problem, for example with integer programming? If so, it would be interesting to know whether this is considerably more efficient than the seeded-EA solution.

- Line 490: this is an important statement, so it should be more clear. The wBCR solutions are still non-dominated "after the challenge" by the EA. Please revise.

- Line 629: Starting from the BCR solutions, could the Pareto front also be filled out by using a finer resolution of the lambda and k variables?


Reviewer #2 Evaluations:
Significant (Required): The paper has some unclear or incomplete reasoning but will likely be a significant contribution with revision and clarification.
Supported (Required): Mostly yes, but some further information and/or data are needed.
Referencing (Required): Yes
Quality (Required): Yes, it is well-written, logically organized, and the figures and tables are appropriate.
Data (Required): Yes
Accurate Key Points (Required): Yes

Reviewer #2 (Formal Review for Authors (shown to authors)):

The paper presents a simulation-multiobjective optimization study to estimate tradeoffs between two environmental objectives (sediment reduction and duck production) given a (large) set of management options and their cost. To reconstruct the Pareto front and analyze tradeoffs, the authors use an evolutionary algorithm with different initialization strategies. The study has two key element that make the analysis interesting: one is that the simulation of sediment production and transport is conducted with a mechanistic, spatially distributed model that takes into account the interdependence of catchment scale processes. This results in interaction between conservation management actions, such that the effectiveness of some practices is affected by the simultaneous adoption of other practices (epistasis, aka nonlinearity, entanglement or other names discussed by the authors). The second element is the analysis of the efficiency of the EA when the search is is initiated with no prior information or initiated with information from points from an initial weighted benefit to cost analysis. 

The paper is relatively straightforward and I did not find any major methodological concerns. I enjoyed reading it. I found the recommendations for practitioners of AE to be very useful, but the paper should go beyond recommending practice. My main comment is that the paper often reads more like a case study or an applications paper than a paper proposing substantial methodological advances. Although the challenges caused by interdependence between decision variables in nonlinear optimization problems and the sensitivity of EA/GA to initial conditions are known, there are a number of interesting and nuanced aspects about these challenges in the paper that I am not sure are clearly highlighted in the introduction. Part of the problems of that feeling that the study may be of limited values is perhaps the relatively frequent caveats (in the abstract, intro and results) that the validity of results can only be guaranteed for this specific study and may not apply to other conditions or models. I appreciate these qualifications and they should be indicated when there are no guarantees that the results are generalizable, but I think that the paper can offer more substantive claims and has sufficient methodological insight to strengthen the introduction and the significance of the paper. 

There is a methodological aspect that I don't understand. Why weren't the inputs to the EA normalized? This may solve the scaling problem between variables mentioned in the text that results in small numbers for one of the objectives. Normalization could also improve and speed up convergence. Normalization using the ratio with the variance of errors offers a simple way to bring data uncertainty information into the analysis. Also, I think the proof in the appendix is incomplete or maybe I am not sharp enough to understand it. Factor Ax in the penultimate equation is not defined. Perhaps it is key to understanding the equality stated in this equation? 

The paper is long and can be significantly tightened to improve focus.


A few minor editorial comments (not exhaustive): 


In page 5, third line point (3) should be "the negative total annual duck hatchling production" since function 1 is minimization. 

Benefit function B in line 196 is not defined before it is presented. 

Lambda weights are not defined after equation (2), they are described in line 402. 

Symbols y and x in quadratic equation (Figure 2b) are used earlier to refer to UTM coordinates. 

Figure 2b is discussed after Figure 3 

Line 472 mentions Figure 4 when I believe it means Figure 2b. 

Table 5 and Figure 5 are discussed in the main text but they are not explicitly referred to. 

Table A.1 is not referred from anywhere in the main text.


Reviewer #3 Evaluations:
Significant (Required): The paper has some unclear or incomplete reasoning but will likely be a significant contribution with revision and clarification.
Supported (Required): Mostly yes, but some further information and/or data are needed.
Referencing (Required): Mostly yes, but some additions are necessary.
Quality (Required): The organization of the manuscript and presentation of the data and results need some improvement.
Data (Required): Yes
Accurate Key Points (Required): Yes

Reviewer #3 (Formal Review for Authors (shown to authors)):

This research addresses two challenges in the design of conservation practices in watersheds: (1) the problem of interdependencies between conservation decisions (i.e. epistatis), and (2) the problem of curse of dimensionality when the number of conservation decisions are extremely large and can limit the effectiveness of a heuristic search algorithm, especially if good initial solutions are not used to initiate the search process. While the overall article is of interest to the readers of this journal, I found this article to be unfocused. For example, early on in the introduction section there is no clarity on the goal of this paper, specifically why and how the problem of epistasis and dimensionality are related and assessed in this work. It is much later in the methods section when a lot of this discussion starts appearing. I list below specific comments and recommendations, which I hope the authors will take into consideration and use them to improve the focus and clarity of their work:
1) Abstract: Please clarify the specific goal of this work - What is the underlying research question that is being pursued? A list the problems and the tasks undertaken in this research are presented, but what were the specific objectives that were pursued in this study to resolve the research problems?
2) Abstract: The authors recommend that seeding with solutions derived from a benefit-to-cost ratio approach can improve the evolutionary algorithm's search process - but insights on why the approach is better are missing.
3) There are quite a few papers published in Ecological Engineering journal (https://www.journals.elsevier.com/ecological-engineering) on this topic, containing insights that will support some of the discussions on optimization of conservation practices and the interdependencies between conservation decisions. I advise the authors to incorporate that body of relevant and important literature in their manuscript. 
4) Why were ducks used as an indicator organism for ecology? Please provide justification. What are the limitations in using ducks versus other organisms? 
5) On page 4, the authors state that "by combining approaches we seek to reduce the overall error associated with optimization." How was this confirmed in this study? Can you clarify whether an overall error was reduced in your results section and conclusions sections?
6) It is unclear as to how large the search space for this problem is. How many decision variables were formulated? Please provide details on the decision variables in your methods section.
7) How were the sediment and duck models validated? How well are the management options simulated in MOSM? Finally, the authors should comment on the potential for errors and underlying uncertainty in these models influencing the extent of epistasis observed.
8) Are the costs in Table 2 and 3 relevant to specific year's data?
9) Section 4.2: It is unclear as to what do the starting seeds look like. Could you use a table or graph to illustrate if there were any patterns in the decisions represented within the seeds?
10) In results section, Section 5.1: What MO decisions were involved in the solutions for cases lambda = 0 to lambda = 1?
11) With regards to solutions shown in Figure 4, did the authors notice any spatial patterns in distributions of costs, sediment, and duck benefits across the watershed landscape?
12) Table 5 and Figure 5 are not referred to anywhere in the text.
13) How are Y axes of Figure 5 calculated?



#### Random thoughts from Sergey:

- Build competence, fake confidence
- fake confidence helps you increase real confidence.  (It is a positive signal to your mind)
- The probability of success will be larger when you have more confidence, conditioning on your competence. 
- Therefore, being confident is always the dominant strategy in any situations.
- Take it as exercises and part of the training in the Ph.D. program. 