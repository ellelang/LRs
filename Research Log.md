Table of Contents**

[TOC]



## December 2018

### 12/06/2018

**Estimate WTA** 

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



**Miscellaneous**

```
cat(paste(shQuote(var_names, type="cmd"), collapse=", "))
cat(paste(var_names, collapse=", "))
```



### 12/07/2018  

- County level income ~ farm size info

 https://finbin.umn.edu/FmSummOpts/Index

- New respondent data entry 

  - enter data in Survey Moneky

  - ENTER data to dataset by hand



### 12/10/2018

- Read the papers of Timothy O. Randhir, Ph.D.

   https://scholar.google.com/citations?user=3_JsdOIAAAAJ&hl=en&oi=sra



### 12/11/2018

- Experiments with dynamic programming algorithms for nonseparable problems
- Experiments with EA  for nonseparable problems for nonlinear fractional knapsack problem.
  - EA with no seeding results
  - EA with Benefit-to-Cost ratio as seeds results
  - The objective function is a nonlinear erosion rates, or see Se Jo's MOSM 

- Python open file 

  ```python
  from pathlib import Path
  mdata_folder = Path("C:/Users/langzx/Desktop/github/EAmosm")
  mosmdata = mdata_folder / "MOSM.accdb"
  ```

- 

- How do I import an .accdb file into Python and use the data?

- Spyder autocomplete 

  ```
  pip install rope_py3k
  ```

- Python select rows based on the value of a specific column

  ```
  df.loc[df['column_name'] == some_value]
  
  ```


### 12/12/2018

- Python slice data --> reset the index, so that the row of each subset dataframe starts from index 0, instead of their index in the original dataframe.

```
SBoutput_LES = SBoutput[SBoutput['Subbasin'] == 4].reset_index(inplace=False)
SBoutput_COB = SBoutput[SBoutput['Subbasin'] == 13].reset_index(inplace=False)
SBoutput_MAP = SBoutput.loc[SBoutput['Subbasin'] == 19].reset_index(inplace=False)
```

 - Set the index for data

 ```
for i in range (0,30):
       for j in range (0,9131):
                index = j + ((i + 1) - 1) * 9131
 ```


 ### 12/13/2018

- Python pandas data print -->show all columns--> by setting the display options

```
pd.set_option('display.max_columns', None)
pd.set_option('display.expand_frame_repr', True) ## if set false, then not a readable table.....
pd.set_option('display.precision', 2)
pd.set_option('display.max_colwidth', 10000)
pd.describe_option('display')
```





### 12/17/2018

- CRP data and possibly useful descriptions 

  [Conservation Reserve Program Statistics - Farm Service Agency](https://www.fsa.usda.gov/programs-and-services/conservation-programs/reports-and-statistics/conservation-reserve-program-statistics/index)

  [www.fsa.usda.gov](http://www.fsa.usda.gov/)

  Updated 2018 CRP Rental Rates and Grassland Rental Rates (New) Map of CRP Enrollment as of March 2016 - Dot Density (pdf). Map of CRP Enrollment as of March 2016 - Color (pdf). Map of Changes in CRP Acreage 2007-2016 (pdf). 49th CRP Signup Results (pdf). 49th CRP County Signup book

  -  https://www.fsa.usda.gov/programs-and-services/conservation-programs/reports-and-statistics/conservation-reserve-program-statistics/index   (updated 2018 CRP Regular Rental Rate)

  [CRP Practices Library - Farm Service Agency](https://www.fsa.usda.gov/programs-and-services/conservation-programs/crp-practices-library/index)

  - Compared the data with cash rental rate from University of Minnesota Extension  https://docs.google.com/spreadsheets/d/1H7gePlOLWOufJWvYJu0UcLdUBHyPhULqHpicRI4HA-I/edit#gid=0

  United States Department of Agriculture Farm Service Agency. United States Department of Agriculture Farm Service Agency. Home; Programs and Services. Aerial Photography. Imagery Products

  - <https://www.fsa.usda.gov/programs-and-services/conservation-programs/crp-practices-library/index>


- Biogeme library 

  [biogeme libarary](http://biogeme.epfl.ch/documentation/html/group__pdfcdf.html#ga2e4416223b57e1063c2d49720912fb62)

- !!!! Multiple sheets in a CSV. file are not supported.!!!!  

  - add a "sheet 2" in the csv. file--> when saving it, it will auto delete the original "sheet 1" . 

- Johnson's SU-distribution 

- Crop rotation in R

  ```R
  dataset0$num_rotation <- as.numeric(dataset$primaryrotation)
  dataset0$convCS <- ifelse(dataset$num_rotation == 1 | dataset$num_rotation == 2, 1, 0)
  dataset0$corn <- ifelse(dataset$num_rotation == 1 | dataset$num_rotation == 2 
                         | dataset$num_rotation == 4 | dataset$num_rotation == 5
                         | dataset$num_rotation == 9, 1, 0)
  ```

- Reshape dataset to wide format

  ```R
  datasetwide1 <- reshape(dataset1, idvar = c("id","task"), timevar = "alti", direction = "wide")
  # where the dataset$alti <- ifelse(dataset$Alternatives == "V",1,2)
  ```


- Left join 

  left_join(x, y): Return all rows from x, and all columns from x and y. If there are multiple matches between x and y, all combination of the matches are returned. This is a mutating join.

  ```R
  datasetwide <- left_join(datasetwide1,dataset_variables, by = c("id.1" = "id"))
  info_id <- idinfo_variables[!duplicated(idinfo_variables), ]
  ```

- Draw exponential distribution from uniform distribution

  https://stackoverflow.com/questions/2106503/pseudorandom-number-generator-exponential-distribution

  Since you have access to a uniform random number generator, generating a random number distributed with other distribution whose CDF you know is easy using the [inversion method](http://en.wikipedia.org/wiki/Inverse_transform_sampling).

  So, generate a uniform random number, `u`, in `[0,1)`, then calculate `x` by:


$$
  x = log (1-u)/\lambda
$$
  where $\lambda$ is the rate parameter of the exponential distribution. Now, `x` is a random number with an exponential distribution. Note that `log` above is `ln`, the natural logarithm.

- Why do some functions have underscores __ before and after the function name?

https://stackoverflow.com/questions/8689964/why-do-some-functions-have-underscores-before-and-after-the-function-name

?          Actually I use _ method names when I need to differ between parent and child class names. I've          read some codes that used this way of creating parent-child classes. As an example I can provide this code:

```python
class ThreadableMixin:
   def start_worker(self):
       threading.Thread(target=self.worker).start()

   def worker(self):
      try:
        self._worker()
    except tornado.web.HTTPError, e:
        self.set_status(e.status_code)
    except:
        logging.error("_worker problem", exc_info=True)
        self.set_status(500)
    tornado.ioloop.IOLoop.instance().add_callback(self.async_callback(self.results))
```

...

and the child that have a _worker method

```python
class Handler(tornado.web.RequestHandler, ThreadableMixin):
   def _worker(self):
      self.res = self.render_string("template.html",
        title = _("Title"),
        data = self.application.db.query("select ... where object_id=%s", self.object_id)
    )
```



- when you use **from x import ***, you actually only imported things in your-python-location/lib/x/\__init__.py

  Packages are folders. Modules are files. If the import calls for specific files then the package folder's \__init\_.py will enumerate the specific files to import.





### 12/18/2018



The second one is a shortcut to the initRepeat() function, fixing its container argument to the creator.Individual class, its func argument to the toolbox.attr_float() function, and its number of repetitions argument to IND_SIZE.

Now, calling toolbox.individual() will call initRepeat() with the fixed arguments and return a complete creator.Individual composed of IND_SIZE floating point numbers with a maximizing single objective fitness attribute.



- Python slice

There is also an optional second clause that we can add that allows us to set how the list's index will increment between the indexes that we've set.

```
a = [1, 2, 3, 4, 5, 6, 7, 8]
a[1:4]
>>> [2,3,4]
```

```
a[1:4:2]
>>> [2,4]
```

That last colon tells Python that we'd like to choose our slicing  increment. By default, Python sets this increment to 1, but that extra colon at the end of the numbers allows us to specify what we want it to be.

```
a[::-1]
>>>[8, 7, 6, 5, 4, 3, 2, 1]
```

 If there is no value before the first colon, it means to start at the beginning index of the list. If there isn't a value after the first colon, it means to go all the way to the end of the list. This saves us time so that we don't have to manually specify len(a) as the ending index.

Okay. And that -1 I snuck in at the end? It means to increment the index every time by -1, meaning it will traverse the list by going backwards. If you wanted the even indexes going backwards, you could skip every second element and set the iteration to -2. Simple.



- zip() in python https://www.geeksforgeeks.org/

```python
# Python code to demonstrate the application of  
# zip() 
 
# initializing list of players. 
players = [ "Sachin", "Sehwag", "Gambhir", "Dravid", "Raina"] 
 
# initializing their scores 
scores = [100, 15, 17, 28, 43]
 
# printing players and scores. 
for pl, sc in zip (players, scores): 
    print ("Player :  %s     Score : %d" %(pl, sc)) 
```

- *args and **kwargs in python explained

https://pythontips.com/2013/08/04/args-and-kwargs-in-python-explained/



- A lambda function https://www.w3schools.com/python/python_lambda.asp

   Lambda is a small anonymous function.

  A lambda function can take any number of arguments, but can only have one expression.

  ```python
  x = lambda a, b : a * b
  print(x(5, 6))
  >>>> 30
  ```

  - Why Use Lambda Functions?
    The power of lambda is better shown when you use them as an anonymous function inside another function.

    Say you have a function definition that takes one argument, and that argument will be multiplied with an unknown number:

    ```python
    def myfunc(n):
      return lambda a : a * n
    
    mydoubler = myfunc(2)
    
    print(mydoubler(11))
    >>>> 22
    ```



- Distribution relies on serialization of objects which is usually done by pickling, thus all **objects that are distributed (functions and arguments, e.g. individuals and parameters) must be pickleable.** This means that modifications made to an object on a distant processing unit will not be made available to the other processing units (including the master one) if it is not explicitly communicated through function arguments and return values.

- In **object**-oriented programming, a **class** is an extensible program-code-template for creating **objects**, providing initial values for state (member variables) and implementations of behavior (member functions or methods)

- &= and ^=

```
ind1 &= ind2                    # Intersection (inplace)
ind2 ^= temp                    # Symmetric Difference (inplace)
```



- Run the whole

  ```python
  def main():
      random.seed(64)
      NGEN = 50
      MU = 50
      LAMBDA = 100
      CXPB = 0.7
      MUTPB = 0.2
      
      pop = toolbox.population(n=MU)
      hof = tools.ParetoFront()
      stats = tools.Statistics(lambda ind: ind.fitness.values)
      stats.register("avg", numpy.mean, axis=0)
      stats.register("std", numpy.std, axis=0)
      stats.register("min", numpy.min, axis=0)
      stats.register("max", numpy.max, axis=0)
      
      algorithms.eaMuPlusLambda(pop, toolbox, MU, LAMBDA, CXPB, MUTPB, NGEN, stats,halloffame=hof)
      
      return pop, stats, hof
                   
  if __name__ == "__main__":
      main()                 
  ```

- Nlogit 

  ```lpj
  
  READ; file="C:\Users\langzx\Desktop\github\DCM\data\wta_observables11192018.csv"; Nobs=7056; Nvar=45; 
  
  Names=id,Y,ChoiceSet,alti,task,Wetland,Payment,Covercrop,NuMgt,incfar,areaf,demPrez16,dem_2018,unemploy,costlive, hrwage,taxcost,cashrent,crp2018,landvalu,impstrea,implakes,impwetl,imptotal,childcar,foodcost,healthc,housecos,othercos,convCS,corn, income_1,income_6,income_4,income_3, income_2,income_NA, income_5, income_7, areaf_1,areaf_2,areaf_4,areaf_3,areaf_NA,areaf_5
  $
  
  dstat; rhs=* $
  
  sample; ALL $
  
  CALC ; Ran(123) $
  
  ? create negative of wetland attribute to estimate lognormal rpl
  
  CREATE ; negWetl = -1*Wetland 
  	 ; lake1000 = implakes/1000
  	 ; agv1000 = landvalu/1000 $
  
  SETPANEL ; Group = ID $
  
  SKIP $
  
  ???? 12/4/18
  ? models with alternative non-negative distributions, not lognormal N-563 in NLOGIT 6 ref guide
  
  sample; 2-7056 $
  
  ?REJECT; income_N = 1 $
  
  nlogit
  ;lhs=Y
  ;Choices=VolCons,Current
  ?;Check Data
  ?; Start = B
  ;Pds = 8
  ?;Panel
  ?;rpl
  ;rpl = lake1000, income_7
  ;Pts = 1000
  ?; Pts = 200
  ;fcn=  -wetland[q],pay(q|#00), covercro(q|#10), nm[q]
  ;Halton
  ;Model:
  
  U(VolCons) = asc + pay*Payment + wetland*Wetland + CoverCro*covercro +	nm*NuMgt + dems18*dem_2018 +  costTax*taxcost +
               incfarm1*income_1 + incfarm2*income_2 + incfarm3*income_3 + incfarm4*income_4 + incfarm5*income_5 + incfarm6*income_6
  		+ farmsi1*areaf_1 + farmsi2*areaf_2 + farmsi3*areaf_3 + farmsi4*areaf_4	+ crp*crp2018		/
  U(Current) = 0
  $
  ```


### 12/19/2018

- NLogit user mannual

  The general format of a command is:

  ```
  VERB; other information . . .$
  ```

  These are separated by semicolons. For example, when you wish to
  compute a regression, you must tell Nlogit what the dependent (LHS) and
  independent (RHS) variables are. You might do this as follows:

  ```
  REGRESS ; LHS = y ; Rhs = One,X $
  ```



  (1) Data analysis

  ```
  dstat; rhs=* $
  DSTATS; RHS = the list of variables $ 
  REGRESS; Lhs = dependent variable; Rhs = independent variable $
  ```

  The * signifies in Nlogit, “all variables.” Thus the command will generate descriptive statistics for all variables within the data set. Inserting specific names (separated by commas) instead of * will generate descriptive statistics only for those variables named.

  ```
  Dstats ; For [ alti ] ; rhs=comfort1,comfort2,ttime $
  ```

  The addition of the ;For[alti] to the Dstats command has Nlogit produce descriptive statistics for the observations that are specific to each value present within the alti variable.

  It may be worthwhile to examine the correlation structure of the data. The command to do so is:

  ```
  Dstats ;rhs=*; Output=2$
  ```



  ```
  LOGIT; Lhs = variable; Rhs = variables$           For a binomial logit model.
  PROBIT; Lhs = variable; Rhs = variables$          For the binomial probit model.
  NLOGIT; various different forms$ 
  CROSSTAB; Lhs = variable; RHS = Variable$
  HISTOGRAM; Rhs = a variable$
  KERNEL; Rhs = one or more variables$
  ```

  Each of these includes many optional features. For example, HISTOGRAM and KERNEL allow different display formats by modifying the command. There are many different kinds of regressions as well.

  (2) Sample setting

  ```
  SAMPLE; first observation – last observation$
  SAMPLE; ALL$ 
  ```

  NOTE: the first rows in the dataset is "missing". So usually  the sample starts from 2 , i.e. 2 to  (n+1)

  ```
  REJECT; decision rule$ 
  ```

  For removing observations from the sample.They are not “deleted.” They are just marked and bypassed until you restore them in the sample. The "REJECT" might cause conflict with the sample number. So need to try.. e.g. SAMPLE; 2 - 7056

  (3) New variables

  ```
  CREATE; name = expression; name = expression . . .$
  ```



  (4) Scientific calculations

  ```
  CALCULATE; expression$
  MATRIX; expression$ 
  ```

  (5) The model estimation

  ```
  NLOGIT
  ;lhs = choice, cset, altij
  ;choices = <names of alternatives>
  ; maxit = n
  ;Model:
  U(<alternative 1 name>) = <utility function 1>/
  U(<alternative 2 name>) = <utility function 2>/
  U(<alternative i name>) = <utility function i>$
  ```

- ```
  Timer$ 
  ```

  Always useful to include this command to see how long it takes to run a
  model

- 

- constant term represents the average influence of unobserved factors influencing choice decisions

An equal change in magnitude in the utility level (e.g., a one unit increase) produced a different change in the magnitude of the change in the choice probabilities. A discrete choice model is non-linear in the probabilities (NB, plotting the probabilities over changes in a utility function, holding everything
else equal, will produce the familiar S-shaped or sigmoid curve; see Figure 11.1).

While the probabilities obtained from a choice model will be non-linear, the utility functions themselves are linear.

Assuming that the original utilities are the true utilities for each alternative, the average utilities for alternatives 1 and 2 are one and zero, respectively (noting that these are relative utilities and hence the average utility for the second alternative is not strictly zero), and the probabilities of choice as calculated from Equation (11.4) for these two alternatives are 0.73 and 0.27 respectively, ceteris paribus.
$$
p_A = \frac{e^1}{e^1 + e^0} = \frac{2.72}{2.72 + 1} = 0.73,\ p_B = \frac{e^0}{e^1 + e^0} = \frac{1}{2.72 + 1} = 0.27\\

p = \frac{e^2}{e^2 + e^0} = \frac{2}{2 + 1} = 0.88\\

p = \frac{e^3}{e^3 + e^0}  = 0.95
$$



### 12/20/2018

- The command set up has two choice models; 
  - the first is the MNL model estimated to obtain the standard set of parameter estimates as well as
    useful additional outputs such as elasticities, partial (or marginal effects) and prediction success; 
  - the second MNL model uses the parameter estimates from the first model to undertake “what if” analysis using **;simulation** and **;scenario**, that involves selecting the relevant alternatives and attributes you want to change to predict the absolute and relative change in the choice shares. Arc
    elasticities can be inferred from the scenario analysis, since it provides before and after choice shares associated with before and after attribute levels

- start point

  ```
  ;Model: U(<alternative 1 name>) = <constant(valuei) > + <parameter(valuej) > *
  <variable> /
  ```

- Constraint value

  ```
  ;Model:
  U(<alternative 1 name>) = <constant[valuei]> + <parameter[valuej]>*<variable>
  ```


- Elasticity 

  The theory underlying the concept of elasticity (or elasticity of choice) was set
  out in Chapter 8. From Louviere et al. (2000, 58), direct and cross-elasticities
  may be defined as:

  > A direct elasticity measures the percentage change in the probability of choosing a
  > particular alternative in the choice set with respect to a given percentage change in an
  > attribute of that same alternative. A cross-elasticity measures the percentage change
  > in the probability of choosing a particular alternative in the choice set with respect to a
  > given percent>age change in a competing alternative.

  - arc elasticity : for dummy variables
  - point elasticity : for continuous variables



  Consider the direct point elasticity for a decision maker given a unit increase in price from $1 to $2 and a decrease in the probability of choice from 0.6 to 0.55.


$$
  E = \frac{0.6 - 0.55}{1 - 2} \times \frac{2}{0.55} = -0.182\\
  E = \frac{0.6 - 0.55}{1 - 2} \times \frac{1}{0.6} = -0.08 \\
  E = \frac{0.6 - 0.55}{1 - 2} \times \frac{1.5}{0.575} = -0.13 \\
$$


  - 

    ```
    ? ;effects: <variablek(alternativei, alternativej)>
    ? ;effects: <variablek(alternativei) / variableh(alternativei)>
    ? 
    ?( ) is for elasticities, [ ] is for partial or marginal effects:
    ;effects:invc(*)/invt2(bs,tr,bw)/invt(cr)/act[bs,tr,bw]
    ;pwt
    ```

  - To use the probability weighted sample enumeration (PWSE) method, the command **;pwt** must also be added to the command syntax.

  ```
  OPEN;export=“C:\Books\DCMPrimer\Second Edition 2010\Latest Version\Data and nlogit set ups\SPRPLabelled\NWelall.csv”$
  Nlogit
  . . .
  ;effects:invc(*)
  ;full
  ?;export=matrix
  ? ;export=tables
  ;export=both
  ;pwt
  . . .$
  ```


- Partial / marginal effects

  A partial or marginal effect reflects the rate of change in one variable relative to the
  rate of change in a second variable. Unlike elasticities, marginal effects are not
  expressed as percentage changes. Rather marginal effects are expressed as unit
  changes. More specifically, we interpret the marginal effect for a choice model as
  the change in probability given a unit change in a variable, ceteris paribus. 

  ```
  ;effects:act[bs,tn,bw];full;pwt
  ```


> As an aside, as the choice probabilities must sum to one, the marginal effects which
> represent the change in the choice probabilities are mathematically constrained to sum to
> zero, thus representing a net zero change over all alternatives. This is not true of elasticities.



- ;simulation command (see Section 13.3.6) to obtain the change in choice shares resulting from a pre specified change in the dummy variable, such as setting gender = 1 and then = 0, and compare the results. Looking ahead, the scenario command would be

  ```
  ;Scenario: gender(bs,tn,bw) = 1.0 & gender(bs,tn,bw) = 0.0 $
  ```


- Confidence Interval:  

  The “confidence interval” shown displays for you the range that contains roughly 95 percent of the sample observations on the elasticities, not a 95 percent confidence interval for a parameter
  estimator.

We can say : 
$$
\mu \in [a,b]
$$
is true in 95% of the samples, OR 

We can say : the interval [a, b] was constructed by a procedure which will output an interval containing $\mu$ in 95% of samples. 

:warning:However, we **can't** say that 
$$
Pr(\mu \in [a,b]) = 0.95 ❌
$$
 Because the interval either does or does not contain \mu, and we do not know whether it does or not. 

 

> If the p-value is less than the analyst determined critical value, we **reject the null hypothesis at the 95 percent level of confidence** and conclude that the mean of the random parameter is statistically different to zero.



- Partial or marginal effects for binary choice

Fundamentally, the model describes the process of choosing one among a set of alternatives and, in response to changes in the attributes such as an increase in cost or travel time, the substitution of one
alternative for another. 

```
logit ; if[altij = 4] ; lhs = choice ; rhs = one,invt,tc,pc,egt $
```

The differences b/w a full MNL model and partial effects model can be explained by two sources: 

1. sampling variability – 175 observations is not a very large sample – 
2.  and the violation of the IIA assumption that we explored in Chapter 7.



- Simulation

1. Estimate the model as previously described (automatically saving outputs
    in memory);
2. Apply the Simulation command (using the stored parameter estimates) to
    test how changes in the attribute and SDC levels impact upon the choice
    probabilities.

Step 1 involves the analyst specifying a choice model that will be used as a basis of comparison for subsequent simulations. The Step 2 involves performing the simulation to test how changes in an attribute or SDC impact upon the choice probabilities for the model estimated in step 1. 

```
simulate ; if[altij=4]; scenario: & tc = 0(.5)10 ; plot(ci)$
simulate ; if[altij=4]; scenario: & tc = 0(.5)10; plot(ci); set:invt=80, pc=30,egt=25$
```

3. scenarios produce **discrete changes in the probabilities from discrete changes in attributes**, it is convenient to compute arc elasticities using the results.

   You can request estimates of **arc elasticities** in ;Simulation by adding ;Arc to the command. Like point elasticities, these be computed either unweighted or **probability weighted by adding ;Pwt** to the command. 

```
Nlogit
;lhs = choice, cset, altij
;choices = bs,tn,bw,cr
;model:
u(bs) = bs + actpt*act + invcpt*invc + invtpt*invt2 + egtpt*egt + trpt*trnf /
u(tn) = tn + actpt*act + invcpt*invc + invtpt*invt2 + egtpt*egt + trpt*trnf /
u(bw) = bw + actpt*act + invcpt*invc + invtpt*invt2 + egtpt*egt + trpt*trnf /
u(cr) =                  invtcar*invt + TC*TC + PC*PC + egtcar*egt
;Simulation;arc
;Scenario: invt2(bs,tn,bw) = 0.9 & invt2(bs,tn,bw) = 0.8 $
```



- Weighting 

  - Firstly, if the information pertains to the true market shares of the alternatives, the weighting criteria to be applied is said to be endogenous, endogenous meaning internal to the choice response. The market shares for the alternatives are represented by the choice variable within the data set. Both endogenous weighting and choice-based sampling is meaningful solely within the context of RP data collection.

  ```
  ;choices = <names of alternatives> / <weight assigned to alt1,> <weight assigned to
  alt2,> . . . , <weight assigned to altj>
  ```



  -  If the information held by the analyst relates to any variable other than the choice variable, the weighting criteria to be applied is said to be exogenous, exogenous meaning external to the system.

  ```
  ;wts = <name of weighting variable>
  ```


- WTP

  ```
  Wald; Parameters = b ; Covariance = varb
  ; Labels = bs,invtz,invtcz,invcqz,tn,bw
  ; fn1 = -(invtz+invtcz*invc) / (invtcz*invt + 2*invcqz*invc)
  ; Means $
  ```

  To compute the mean WTP, the function would be computed for each observation in the sample and the functions would be averaged. This calculation can be obtained by removing ;Means from the command above. An alternative to the delta method is the Krinsky–Robb (K&R) method. The preceding

  ```
  ;K&R ; Draws = number
  ```



### 12/21/2018

- Once the analyst is content with the model results, the model should be **re-estimated with a greater number of draws to confirm stability in the results.**

> As an aside, the statistical significance of attributes does vary as the number of draws
> changes, so one must exercise some judgment in the initial determination of statistically
> significant effects. Practical experience suggests that an attribute with a z-value over 1.5 for
> a small number of draws may indeed become statistically significant (i.e., over 1.96) with a larger number of draws. This has been observed more for the standard deviation parameters
> (i.e., those derived from normal and log-normal distributions).



- Kernel function 

what the kernel density function is measuring **is the proportion of the sample of values that is close to the chosen zj.** 

The kernel density function for a single attribute is computed using Equation :
$$
f(z_j) = \frac{1}{n}\sum^n_{i = 1} \frac{K[(z_j - x_i)/h]}{h}, j= 1, ...,M.
$$
The function is computed for a specified set of values of interest, zj, j = 1,. . .,M where zj is a partition of the range of the attribute. Each value requires a sum over the full sample of n values, xi, i = 1....n. The primary component of the computation is the kernel, or weighting function, K[.], which take a number of forms. For example, the normal kernel is K[z]= φ(z) (normal density). Thus, for the normal kernel, the weights range from φ(0) = 0.399 when xi = zj to values approaching zero when xi is far from zj. 



The other essential part of the computation is the smoothing (bandwidth) parameter, h, to ensure a good plot resolution. The bandwidth parameter is exactly analogous to the bin width in a common histogram. Thus, as noted earlier, narrower bins (smaller bandwidths) produce unstable histograms (kernel density estimators) because not many points are “in the neighborhood” of the value of interest. Large values of h stabilize the function, but tend to flatten it and reduce the resolution. 

An example of a bandwidth is given in Equation (15.7), which is a standard form used in several contemporary computer programs:
$$
h = 0.9Q/n^{0.2}
$$
 where Q = min(standard deviation, range/1.5).

A number of points have to be specified. The set of points zj is (for any number of points) defined by Equation:
$$
z_j = z_{LOWER} + j\times [(z_{UPPER}- z_{LOWER})/M], j = 1, ..., M\\
z_{LOWER} = min (x) - h\\
z_{UPPER} = max (x) + h
$$
The procedure produces an M× 2 matrix in which the first column contains zj and the second column contains the values of f(zj) and the **plot of the second column against the first – this is the estimated density function.**

```
;kernel;rhs=<name of parameter/variable>;Limits=<lower, upper values>;<model form>$
e.g., 
kernel;rhs=invtd;limits=0,1.5;logit$.
```



- heterogeneity in the mean of random parameters

- heterogeneity in the mean of selective random parameters

- heteroskedasticity and heterogeneity in the variances

   So far, we have focussed on heterogeneity in the mean of a random parameter; however, additional sources of systematic heterogeneity (often referred to as heteroskedasticity) can be associated with the variance (or standard deviation) of the distribution.



### 12/22/2018

- Unconditional parameters 
  - The ML output generated by Nlogit (as reported and discussed in previous sections of this chapter) is that of the unconditional parameter estimates. The output shown is representative of the entire sampled population. The output provides the mean and standard deviation of each of the random parameter distributions. As such, in using the unconditional parameter estimates, the specific location on the distribution for any given individual is unknown. If, however, one is also interested in determining the presence of heterogeneity in the sampled population and the possible sources of heterogeneity, as shown in previous sections, then the ML model is ideal.
  -  In summary, the unconditional parameter estimates capture information on (1) the distributional form of the marginal utilities of each random parameter (specified by the analyst), (2) the means of the distributions, and (3) the dispersion of the distributions provided in the output as the standard deviation or spread parameters. 





- how to estimate the conditional parameter estimates (i.e., individual specific parameter estimates conditioned on the choices observed within the data) that may be used to decide where on the distribution (of marginal utility) an individual resides. These individual parameter estimates may then be used to derive individual level outputs, such as WTP measures (which can themselves be directly calculated as a distribution), elasticities, etc., or be exported to other systems such as a larger network model.

  >  The use of these individual parameter estimates, while scientifically rigorous
  > (they are obtained Bayesian like, conditioned on the choice data), means that any output
  > generated is limited to within the sample drawn as part of the study. Prediction outside of the sample is not possible unless one has a very robust set of mapping variables to assign a hold out sample observation to an observation used in the model estimation. Thus, if the analyst wishes to predict outside of the sample, the unconditional parameter estimates are usually preferred (see Jones and Hensher 2004).

- Individual-specific parameter estimates: conditional parameters

  - Rather than rely on randomly allocating each sampled individual within a distribution
    as a way of allocating preference information, it is possible to utilize the additional information about the choices each individual was observed to have made as a way of increasing the accuracy of the preference allocation

- The stored matrices of mean and standard deviation conditional parameter estimates provide important data to use in obtaining the distributions of random parameters that are conditioned on each respondent’s choice. There are many ways in which such evidence can be presented, but the most appealing method is one that can graphically show the distribution as well as indicate the confidence interval.

- As a general result, an interval in a distribution for a continuous random variable defined by the mean plus and minus two standard deviations will encompass 95 percent or more of the mass of the distribution. This enables us to form a sort of confidence interval for βi itself, conditioned on all the information known about the individual. To obtain this level of confidence, the interval:



### 12/26/2018 

- Likelihood ratio test
  - LR = 2 (log L | unrestricted model -  log L | restricted model)

The LL for the nested logit is -199.25552. The LL for the MNL is -200.40253. Twice the difference is the estimated Chi squared statistic, which is only 2.294. With two degrees of freedom, the critical value (95 percent) is 5.99. **So the hypothesis of the MNL model is not rejected by this test**. The LL function for the nested logit model is not significantly larger than that for the MNL model:

- Wald test
  - The Wald distance is a measure of the distance of the estimated parameters from the hypothesized values. A familiar example is the simple t test of how far an estimated parameter is from zero (or, in the case of nested logit, how far the inclusive parameter estimate is from 1.0). The Wald statistic is computed as a quadratic form in the distance of the parameters from the null hypothesis using the inverse of the appropriate covariance matrix. The statistic has a Chi-squared distribution with degrees of freedom equal to the number of restrictions

- Lagrange multiplier test
  - The Lagrange multiplier (LM) test is a test of the hypothesis that these derivatives are actually “close” to zero. It is a Wald statistic based on the derivatives of the criterion function. The LM statistic is a Chisquared statistic with degrees of freedom equal to the number of restrictions.



> IIA assumption :  irrelevant alternatives (IIA)
>
> RP : revealed preference 



- Variance estimation

  Statistical inference, such as some hypothesis tests, confidence intervals, and estimation generally, relies on computation of variances of estimators. There are several ways to proceed. The starting point is the estimator of the asymptotic covariance matrix of the estimator of the model parameters.


  Central to this activity is the information obtained from a variance-covariance matrix of parameter estimates. 

  - **The conventional estimator** of the covariance matrix of b is the negative inverse of the second derivatives matrix.

  - **Robust estimation,** e.g. White estimator, that appropriately estimates the asymptotic covariance matrix of the ordinary (unweighted) least squares estimator, even in the presence of heteroskedasticity. 

  - **Bootstrapping** of standard errors and confidence intervals

    - Bootstrapping is a technique used to deduce the properties (usually mean and variance) of the sampling distributions of estimators by using the variation in the observed sample under an assumption that the pattern of variation in the observed sample mimics reasonably accurately the counterpart in the population.

      In many cases, it is uncertain what formula should be used to compute the asymptotic covariance matrix of an estimator. In these cases, a more reliable and common strategy is to use **a parametric bootstrap procedure** instead. This requires **drawing from the estimated asymptotic distribution of the parameter estimates, and computing the non-linear function for each independent draw.** If this process is repeated many times, any feature of the sampling distribution of the non-linear function can be accurately estimated. Since the moments of these distributions may not exist, confidence regions should be estimated directly using percentiles of the sampling distribution.

    - More intuitively, the idea is as follows. We typically have just one data set. When we compute a statistic on the data, we only know that one statistic (e.g., some mean estimate of WTP); we do not see how variable that statistic is. The bootstrap creates a large number of datasets (say, R repetitions) that we might have seen and computes the statistic on each of these data sets. Thus we get a distribution of the statistic. The strategy to create data that “we might have seen” is key.

    - Note in the execute command that generates the bootstraps, we have accounted for the fact that in this sampling setting an “observation” consists of “cset” rows of data

- Variances of functions and willingness to pay

  Estimated parameters are not individually useful. Because the scale of the error terms is not identified, the scale of the individual parameters is also not identified. Therefore we typically look at ratios of the parameters (usually identifying willingness to pay (WTP) in the model), or use the parameters to carry out demand simulations. 

  - If the parameter estimates are uncorrelated, then the ratios will typically have a Cauchy distribution (which has no finite
    moments). This fact suggests that standard delta-method approximations (see above and
    also Greene 1997, 127 and 916) will not yield reliable inferences, although the resulting
    standard error estimates are certainly better than nothing!
  - This section is concerned with **methods of obtaining asymptotic covariance matrices for estimators** such as these. Two equally effective and widely used methods are the delta method  and the Krinsky–Robb (KR) method. The standard errors for a WTP ratio are defined as in Equation


$$
   s.e._{(\frac{\beta_k}{\beta_c})} \approx \sqrt{\frac{1}{\beta_c^2}[Var(\beta_k) - \frac{2\beta_k}{\beta_c}Cov(\beta_k,\beta_c) + (\frac{\beta_k}{\beta_c})^2Var(\beta_c)]}
$$

  - Delta Method
  - Non-symmetric confidence intervals obtained using Krinsky-Robb (KR )simulations are recommended
    - 1. Estimate the WTP model with any function form. 
      2. obtain the vector of parameter estimates and the VCV matrix  V(est $\beta$)
      3. Calculate the Cholesky decomposition, C, of the VCV matrix such that CC'=V(est $\beta$).
      4. Randomly draw from standard normal distribution a vector x with k independent elements.
      5. Calculate a new vector of parameter estimates Z such that Z =$\beta$+C'x.
      6. Use the new vector Z to calculate the WTP measures.
      7. Repeat steps 4, 5, and 6 N (e.g., >=5,000) times to obtain an empirical distribution of WTP.
      8. Sort the N values of the WTP function in ascending order.
      9. Obtain a 95 percent confidence interval around the mean/median by dropping the top and bottom 2.5 percent of the observations.

- Bayesian 

  The key difference between Bayesian and classical approaches is that Bayesians treat the nature of the randomness differently. In the classical view, the randomness is part of the model; it is the heterogeneity of the taste parameters, across individuals. In the Bayesian approach, the randomness ‘represents’ the uncertainty in the mind of the analyst (conjugate priors notwithstanding).
  Therefore, from the classical viewpoint, there is a ‘true’ distribution of the parameters across individuals. From the Bayesian viewpoint, in principle, there could be two analysts with different, both legitimate, but substantially different priors, who therefore could obtain very different, albeit both legitimate, posteriors.

  Prior knowledge about parameters, θ, is gathered in a prior distribution, π(θ). T**he sampling distribution, or likelihood function, is given by f(X|θ)** where X contains all the sample data in the study. After observing the data, the information about θ is given by the posterior distribution which is derived using Bayes Theorem:
  $$
  Pr(\theta | x) = \frac{f(x|\theta)\pi(\theta)}{
      \int f(x|\theta)\pi(\theta)d\theta
  }
  $$

  - We note for the purposes explained below, that the posterior density is functionally equivalent to the conditional distribution of the parameters given the data. All inference is based on this posterior distribution. The usual Bayes estimator is the mean of the posterior distribution, and Bayesian confidence bands are typically given by the narrowest region of the posterior distribution with the specified coverage probability. Bayesian confidence regions are interpreted as fixed regions containing the random parameter θ with the specified coverage probability (i.e., the ‘highest posterior density’ interval). This is different from the classical confidence region, which is a region with random endpoints that contain the true value θ with the specified probability over independent repeated realisations of the data (Brownstone, 2001). Classical inference therefore depends on the distribution of unobserved realizations of the data, whereas Bayesian inference conditions on the observed data. Bayesian posterior inference is also exact and does not rely on asymptotic approximations to a true sampling distribution.

 The ability to combine information about the aggregate distributions of preferences with individuals’ choices to derive conditional estimates of the individual parameters is very attractivese :flushed:



### 12/31/2018

- Latex alignment equation only one line number--> add the  "\nonumber"
- turn off section numbering in latex "\section*{Special relativity}"



##  January 2019



### 1/2/2019 

- LaTeX/Special Characters  \hat, \bar, \tilde

  https://tex.stackexchange.com/questions/66537/making-hats-and-other-accents-bold

- Choice experimental design

  *"A_primer on nonmarket valuation"*

  The basic problem addressed in the experimental design literature for CEs—given the selected attributes and their levels—is how to allocate attribute levels to alternatives and choice sets. Several approaches to experimental design for CEs have been proposed, and the best approach to use depends on which preference parameters need to be estimated and whether or not prior information on the parameters is available. The researcher also needs to think about the complexity of the design because the inclusion of many alternatives and choice sets can cause respondents to use decision-making shortcuts (heuristics) that might not reflect their true preferences.

   An experimental design must contain sufficient independent variation among attribute levels within and across alternatives so that each preference parameter can be identified. For example, if the levels of an attribute are always identical across alternatives, it will not be possible to identify the effect of that attribute on responses. A good design is also statistically efficient, meaning it minimizes (maximizes) the standard errors (precision) of the preference parameter estimates.

  - Orthogonal full factorial design

    - The primary advantage of a full factorial design is that all main and interaction effects are statistically independent (orthogonal) and can be identified when estimating a model

    - The major drawback of this design is that a very large number of alternatives are generated as the numbers of attributes and levels are increased. If each of these three attributes takes two levels (install or not for Picnic shelters, install or not for Boat ramps, $10 or $20 for camping fees), there are 2^3 = 8 possible combinations of attribute levels in the full factorial design.  If the number of levels associated with each attribute increases from two to three, the full factorial design increases to 3^3 = 27 possible combinations of attribute levels.

  - Orthogonal Fractional Factorial Designs

    - The simplest method of generating a fractional factorial design is to select subsets of attribute combinations from the full factorial design using higher order interaction terms 
    - However, in reducing the design size, fractional factorial designs omit some or all information on interaction effects. If the omitted interactions are important in explaining responses, the preference parameter estimates may be biased due to confounding an omitted variable with a main effect.
    - Due to the possibility that a fractional factorial design can induce biased parameter estimates on the main effects and can fail to identify meaningful interactions, it is essential to identify which attribute interactions might be important during the design stage of survey development.
    - These potentially important interactions could be evaluated by asking focus group participants if some combinations of attribute levels are particularly desirable or undesirable. If so, a main effects plus selected interactions plan should be used. In general, this is accomplished using orthogonal codes to examine the correlations between the main and interaction effects and assigning attributes to design columns that are orthogonal to the specified interaction effects



  - Generating Choice Sets for Orthogonal Designs

    The key issues to consider in creating an experimental design for a CE are how to place alternatives into choice sets and how many choice sets are needed.

    - the number of choice sets depends on the number of degrees of freedom (the number of parameters plus one) required to identify the parameters of the specified model.
    -  the number of degrees of freedom depends on whether the alternatives are described using a label to differentiate the alternatives (such as transportation modes or recreational locations) or whether they are unlabeled (generic). 
    - Labeled alternatives are used when the researcher wants to estimate a utility function for each alternative. 
    - The ability to identify the independent effect of each attribute in each alternative requires that attributes are orthogonal within and between alternatives. Unlabeled alternatives are used when the researcher is only interested in estimating a single utility function. Because labeled designs require more parameters to be estimated, more degrees of freedom are required, resulting in a larger design.
    - the alternative specific constants provide a means for measuring that component of
      utility that is independent of the experimentally designed attributes. It is also common to test for status quo bias in unlabeled designs by including an alternative specific constant for the status quo alternative. If the alternative specific constant is statistically significant, it suggests that respondents have a preference for (or against) the status quo option independent of the designed attributes.
    - For unlabeled alternatives in which the analyst wants to estimate nonlinear effects, the **minimum degrees of freedom required is (L − 1) x A + 1,** where L is the number of attribute levels and A is the number of attributes. If only one parameter is estimated for each attribute, the number of degrees of freedom is reduced to A + 1. For labeled alternatives, the comparable
      formulas are (L − 1) x NA + 1 and NA + 1, where N is the number of alternatives.
    - Because choice models are based on attribute differences, the lack of a contrast for attribute levels within choice sets reduces the statistical efficiency of the design.
    - In general, randomizing attribute combinations will be inadequate for estimating independent utility functions for labeled alternatives because the attributes will not be orthogonal across alternatives, and main effects will be correlated (Hensher et al. 2005; Street et al. 2005).

  - Statistical Efficiency for CEs

    Traditional orthogonal designs were developed for linear-in-parameters statistical models and meet two criteria for good designs: (1) they remove multicollinearity among attributes so that the independent influence of each attribute can be estimated, and (2) they minimize the variance of the parameter estimates so that t-ratios (based on the square roots of the variances) are maximized. These design criteria are met when the elements of the variance-covariance matrix for the linear model are minimized (Rose and Bliemer 2009).

    - "best" variance-covariance matrix --> A commonly used summary statistic for the information contained in the variance-covariance matrix is the determinant as it uses information on the main
      diagonal (variances) and the off-diagonals (covariances). The determinant of a variance-covariance matrix, scaled by the number of parameters to be estimated in the model, is known as the D-error. Designs that minimize the D-error are considered to be **D-efficient**. 

    - - Optimal Orthogonal Designs 

        One approach for finding D-efficient designs for CEs is to assume that all alternatives contained in choice sets are equally attractive or, equivalently, that all preference parameters equal zero. These designs are referred to as optimal orthogonal designs. In general, a D-efficient optimal orthogonal design is constructed by minimizing
        the following expression
        $$
        D_0-error = det(VC(Z, 0))^{\frac{1}{k}}
        $$
        where Z represents the attributes in the experimental design, 0 indicates that beta = 0 for all model parameters, and k is the number of parameters used in the scaling factor. (The smaller of the D_p, the better of the design)



      - Nonzero Priors Designs
    
        A second approach to the efficient design of CEs using the variance-covariance matrix is based on the idea that information about the vector of preference parameters might be available from pretests or pilot studies and that this information should be incorporated in the design This approach, which we call a nonzero priors design, seeks to minimize the following expression:
        $$
        D_p-error = det(VC(Z, \beta))^{\frac{1}{k}}
        $$
        where p stands for the point estimates of the (nonzero) b’s. The constraints imposed
        on the optimal orthogonal model (orthogonality, attribute level balance, and minimal
        overlap) are relaxed in minimizing the Dp-error. However, if reasonable nonzero
        priors are available, relaxing these constraints can result in efficient designs that
        greatly reduce the number of respondents needed to achieve a given level of significance
        for the parameter estimates (Huber and Zwerina 1996). Note that designs
        that minimize the Dp-error do not generally minimize the D0-error and vice versa.
    
        If the nonzero priors are incorrect, however, the selected design will not be the most efficient. 
    
        - One method for evaluating this potential shortcoming is to test the sensitivity of a D-efficient design to alternative parameter values, which can provide the analyst some degree of confidence about the robustness of a design (Rose and Bliemer 2009).
        - Another approach that can incorporate the analyst’s uncertainty about parameter values is to **specify a distribution of plausible values that reflects subjective beliefs about the probabilities that specific parameter values occur** (Sándor and Wedel 2001; Kessels et al. 2008). This Bayesian approach to experimental design proceeds by evaluating the efficiency of a design over many draws from the prior parameter distributions $ f(\tilde{\beta})$. The design that minimizes the expected value of the determinant shown in Eq below is a D-efficient Bayesian design:
    
        $$
        D_b-error = \int_{\tilde{\beta}} det(VC(Z, \tilde{\beta}))f(\tilde{\beta})d\beta
        $$


  - Selecting a design

    Given a suite of alternative design options, which design should a researcher choose? **Although this will depend on considerations specific to each study, the authors recommend the following general guidelines.** 

    - First, use a design that is statistically efficient in the context of the nonlinear-in-parameters models used to analyze random utility models. If reasonable information is available on preference parameters from sources such as pretests or pilot studies, the authors recommend using a nonzero priors design. In general, these designs reduce the number of respondents needed to achieve a specific precision (standard error) for the parameters specified in the utility function(s) and can therefore help reduce the cost of survey implementation.
    -  In cases where no prior information is available or where parameter estimates from other CE studies do not provide a good match, an optimal orthogonal design should be considered. This recommendation is based on evidence that optimal orthogonal designs can produce good results where prior information on parameter values is of poor quality or when the model specification chosen by the analyst is inconsistent with the underlying data generating process (Ferrini and Scarpa 2007). The construction of statistically efficient designs is greatly facilitated by the availability of software programs (such as SAS and Ngene).



### 1/3/2019 

- ASCs 
  alternative-specific constants (ASCs) 

- IRB APPLICATION (MRB Survey see notes in Evernote)

- Human subjects approval for the survey was granted by the Human Subjects Review Board at the University of Washington.

- Refer table /figure in latex

  ```
  \begin{figure}[here]
  \includegraphics[width=0.9\textwidth]{images/JobInformationDialog.jpg}
  \caption{A prototype of the Job Information dialog}
  \label{fig:jobInformationDialog}
  \end{figure}
  
  -->>>>> Please see Figure ~\ref{fig:JobInformationDialog} on page ~\pageref{fig:JobInformationDialog} for a prototype blah blah blah
  
  
  ################
  \begin{table}[!htb]
      \centering
          \begin{tabular}{lrc}\hline
          ....
      \caption{Class Mark List}\label{tab:a}
  \end{table}
  ```



### 1/4/2019



- Why use .sty file?   https://tex.stackexchange.com/questions/91167/why-use-sty-files
- https://tex.stackexchange.com/questions/528/style-class-tutorials
- How to write a class file https://www.dickimaw-books.com/latex/admin/html/clsform.shtml

First of all: *never* use `\include` to load a file with personal definitions and packages to use.

The choice is thus between `\input` and `\usepackage`; for the first it's better to use the extension `.tex` for the file, for the second `.sty` is mandatory.

What are the pros of the latter solution? Many. For instance you can define *options* that can change the behavior of your macros or selectively load parts of it.

In a `.sty` file `@` is assumed to be a letter, so no `\makeatletter` or `\makeatother` command is needed to access "private macros", which is often the case for complex macros.

If you don't need options nor access to private macros, loading your definitions and package with `\input{mymacros}` is exactly equivalent to `\usepackage{mymacros}` (provided that the file is `mymacros.tex` in the first case and `mymacros.sty` in the second one).

As noticed by Andrew Stacey, there is one more pro in using a `.sty` file: it won't be loaded twice, even if called twice in a document (maybe frome some other loaded file or package). This is important because `\newcommand` would raise errors on the second loading (and other definitions might lead to infinite loops).

Example. Suppose you have a macro that must change its behavior when the `draft` option is enabled in the `\documentclass` line; for instance it should have an argument that's emphasized in the text and is also written in the margin for draft copies.

Example. Suppose you have a macro that must change its behavior when the `draft` option is enabled in the `\documentclass` line; for instance it should have an argument that's emphasized in the text and is also written in the margin for draft copies.

```tex
\ProvidesPackage{mymacros}
\newif\if@myfiledraft
\DeclareOption{draft}{\@myfiledrafttrue}

\ProcessOptions\relax

\if@myfiledraft
  \newcommand{\myterm}[1]{\emph{#1}\marginpar{TERM: #1}}
\else
  \newcommand{\myterm}[1]{\emph{#1}}
\fi

\endinput
```

If a document does

```tex
\documentclass[draft]{article}
\usepackage{mymacros}

\begin{document}
\term{foo}
\end{document}
```

then "TERM: foo" will be written in the margin. If `draft` is removed, the same source will only emphasize "foo" in the text.



- Latex beamer theme

  https://hartwork.org/beamer-theme-matrix/

- 

### 1/10/2019

- Model 4: heterogeneity in the mean of random parameters

The distributions derived from the estimated random parameters are defined in terms of the full sample, and each respondent is randomly assigned an estimate drawn from the full distribution. While this avoids the need to be concerned about where a particular respondent might best be located on the distribution, it runs the real risk of missing out on an opportunity to establish whether a specific sampled respondent might be at the upper or lower part of the distribution as a consequence of some additional systematic source of influence. 

The opportunity to assess whether such systematic sources exist is referred to as adding an additional layer of heterogeneity, which may be associated with the mean of the distribution and/or the variance (or standard deviation) of the distribution. In this section, we introduce heterogeneity in the mean of a random parameter.

**To introduce heterogeneity around the mean** we have to include the ;rpl command and add to it “=name of heterogeneity influence.” In the application below we have added in the socio-economic effects ;rpl=pinc. If that is all that is included as an extra command**, then every random parameter will be conditioned on the personal income** of a respondent, which is essentially an interaction term such that the new expression for the marginal utility of an attribute. 

Note that when you have a heterogenous mean, this construction becomes somewhat ambiguous. For the specification above, for example, if the uniform distribution were specified, the range of variation of the parameter, for a given value of income, is from δ_{pinc} to δ_{pinc} + 2β. The uniform and triangular distributions with value = 1 are special cases, as this device allows you to anchor the distribution at zero for this case. Importantly, however, **when you**
**impose a constrained distribution on a random parameter, the inclusion of an additional term to allow for systematic heterogeneity no longer guarantees that the sign or range condition holds.**

The model below is an extension of the previous model, with the addition of the 11 parameters associated with heterogeneity in the mean of the random parameters. The LL at convergence is −2444.458, compared to −2465.752 for exactly the same model without these additional parameters. With 11 degrees of freedom difference, the LRT gives −2*(21.294) = 42.588. This is greater than the critical Chi-square value with 11 degrees of freedom of 19.68, and hence
we can reject the null hypothesis of no difference:

```
Nlogit
;lhs=resp1,cset,Altij
;choices=NLRail,NHRail,NBway,Bus,Bway,Train,Car
;par
;rpl=pinc
;fcn=invt(t,1),cost(t,1),acwt(t,1) ,eggt(t,1), crpark(t,1),
accbusf(t,1),waittb(t,1],acctb(t,1),crcost(t,1),crinvt(t,1),creggt
(t,1)
;maxit=200
;halton;pts= 100
;model:
$
```

The marginal utility associated with a specific variable now includes the additional “interaction” term. For example, the marginal utility expressionfor invt is: 

MUinvt = − 0.07373 + 0.0001**pinc + 0.07373*o,

 where o is the one-sided triangular distribution. This additional term indicates that as personal income increases, the marginal utility of invt will increase or the marginal disutility (given the negative sign for the mean estimate) will decrease. 



- Model 5: heterogeneity in the mean of selective random parameters
  Model

Model 4 allows for heterogeneity in the mean to be identified for all random parameters. It is often the situation that the analyst wants to limit the heterogeneity to a subset of random parameters, either for some behaviorally interesting reason or because the heterogeneity was found to be not statistically significant for specific random parameters. ML permits a specification that controls for selective use of heterogeneity in the mean.

We begin with a general variation in the form for name (type) such as
invt(n) used in earlier models, which is name (type|#) or invt (n|#). This
simply says that all random parameters will not have an interaction term to
allow for heterogeneity in the mean, where the heterogeneity is defined by one
or more variables associated with the command ;rpl=hetvar1, hetvar2. . ... That
is, where we have name (type), heterogeneity will apply; **where we have name**
**(type|#), it will not apply.** 



If we want to limit the heterogeneity in the mean to a subset of attributes then we would define a pattern of 0s and 1s, where 1 includes the heterogeneity and 0 does not for the set of hetvars associated with ;rpl. For example, if we specify (as below) **;rpl=pinc,gender**, and we want to include pinc but not gender, then we would specify name (type#10) – for example, acwt(t|#10). It should be clear that acwt(t|#00) excludes both sources of heterogeneity, and acwt(t|#11) includes both sources of heterogeneity; thus acwt(t|#00) is equivalent to acwt(t|#).



; Fcn = invt(n,1) says the
σinvt = 1 * |βinvt|. The parameter that enters the absolute value function is the constant term in the parameter mean.



```
Nlogit
;lhs=resp1,cset,Altij
;choices=NLRail,NHRail,NBway,Bus,Bway,Train,Car
;par
;rpl=pinc,gender
;fcn=invt(t,1),cost(t,1),acwt(t|#10) ,eggt(t|#11), crpark(t|#11),
accbusf(t,1),waittb(t|#00),acctb(t|#10),crcost(t|#00),crinvt(t,1),
creggt(t|#01)
;maxit=200
;halton;pts= 100
;model:
U(NLRail)= NLRAsc + cost*tcost + invt*InvTime + acwt*wait+ acwt*acctim
+ accbusf*accbusf+eggT*egresst + ptinc*pinc + ptgend*gender +
NLRinsde*inside /
U(NHRail)= TNAsc + cost*Tcost + invt*InvTime + acwt*WaitT + acwt*acctim
```



- Model 6: heteroskedasticity and heterogeneity in the variances

So far, we have focused on heterogeneity in the mean of a random parameter; however, additional sources of systematic heterogeneity (often referred to as heteroskedasticity) can be associated with the variance (or standard deviation) of the distribution.

When the model is expanded so that the random parameters model allows heterogeneity in the variances as well as in the means in the distributions of the random parameters, the additional modification is σik = σk exp[ωk'hri]. If ω equals 0, this returns the homoscedastic model. The implied form of the RPL model is:
$$
\beta_{ik} = \beta + \delta_{k'}z_i + \sigma_{ik}v_{ik} =  \beta + \delta_{k'}z_i + \sigma_kexp(w_{k'}\text{hr}_i)v_{ik}
$$
The variables in **hr_i** may be any variables, but they must be choice invariant. This specification will produce the same form of heteroskedasticity in each parameter distribution – note that each parameter has its own parameter vector, ωk. 

we described the method of modifying the specification of the heterogenous means of the parameters so that some RPL variables in **zi** may appear in the means of some parameters and not others. A similar construction may be used for the variances. For any parameter specification of the forms set out above, the specification may end with an exclamation
point, “!” to indicate that the particular parameter is to be homoskedastic even if others are heteroskedastic. For example, the following produces a model with heterogenous means (associated with age and pinc), and one heteroskedastic variance (associated with gender):

```
; RPL= age,pinc
; Hfr = gender,family,urban
; Fcn = invt(n),acwt(n|# 01 ! 101)
```

The variance for invt includes all three variables, but the variance for acwt excludes family.

- Model 7: allowing for correlated random parameters

The previous models assume that the random parameters are uncorrelated. As discussed in Chapter 4, all data sets, regardless of the number of choice situations per sampled individual (i.e., choice sets), may have unobserved effects that are correlated among alternatives in a given choice situation. ML models enable the model to be specified in such a way that the error components in different choice situations from a given individual are correlated.

> As an aside, The model with both correlated parameters (;Correlated) and heteroskedastic
> random parameters is not estimable. If your model command contains both ;Correlated and ;Hfr = list, the heteroskedasticity takes precedence, and ;Correlated is ignored

The following ML model is estimated allowing for correlation among the
random parameters of the model:





- N29: Random Parameters Logit Model N-563

The exponential random variable has a mean of one, so the mean of the
parameter distribution in this case is b. Note that in all four cases, we are restricting the shape of the distribution as well as the mean and variance. The first three of these are likely to be attractive alternatives to the lognormal distribution. Finally, the triangle and uniform distributions are constructed so that the spread parameter equals the mean parameter. This construction is described in the next section. The beta model is likely to be an attractive alternative to the triangle and uniform models because of the smoothness of the distribution.



- From GMNL instructions

- GMNL formula
  a symbolic description of the model to be estimated. The formula is divided in five parts, 
  each of them separated by the symbol |. 
  - The first part is reserved for alternative-specific variables with a generic coefficient.
  - The second part corresponds to individual-specific variables with an alternative specific coefficients. 
  - The third part corresponds to alternative-specific variables with an alternative-specific coefficient. (e.g. income is only related to the choice of Train, not for Air and Bus)
  - The fourth part is reserved for time-invariant variables that modify the mean of the random parameters.  (e.g. late1000 modified the mean of  the distribution of Covercrop coefficients) 
  - Finally, the fifth part is reserved for time-invariant variables that enter in the scale coefficient or in the probability assignment in models with latent classes.
     (from gmnl help)

Part three: "alternative-specific variables with an alternative-specific coefficient." --> not fixed numbers, but a distribution with mean and sd.



### 1/11/2019

Pseudo-R square = 
$$
1 - \frac{log L(model)}{log L(base model)}
$$
where the base model would be a model that contains only a constant term. For any binary choice model, the base model would have

log L_0 = N1



### 1/12/2019

- Latex bookmark issue

  ```latex
  \setcounter{secnumdepth}{0} 
  %don't show the section number
  %% if you use \section*{}, no bookmarks show on the pdf file
  ```



- Export Nlogit results to spreadsheet P 385

Model results and estimated partial effects or elasticities may be exported to a spreadsheet
file. Before doing this, you must open the export file with

```
OPEN ; Export = “C:\… \elasticities.csv” $
CLOGIT ; Lhs = mode; Choices = air,train,bus,car
; Rhs = gc,ttme,invc,invt ; Rh2=one,hinc
; Export output
; Export = table
;?Export = matrix
; Effects: gc(*),ttme(*) ; Full $
```



- KR simulation

  The primary difficulty in carrying out the Krinsky and Robb procedure is getting the N parameter vector draws from the multivariate normal distribution.

  To execute the Krinsky-Robb procedure, draw N observations on the parameter vector \beta from the estimated multivariate normal distribution of the parameters.

- csv file can't have multiple sheets!!! Need to use xsl. to restore sheets!!!



### 1/15/2019

For the current RPL specification, with exponential distribution and a fixed parameter, K&R should be quite straightforward.


As an aside, think about how you might use the uncertainty of WTA at a specific location to say something about practices/locations which may be robust to cost assumptions.



Nlogit6 P548. exponential distribution, scaled: 
$$
\beta_i = \beta v_i, \ v_i \sim exponential
$$
