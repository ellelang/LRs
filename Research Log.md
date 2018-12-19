**Table of Contents**

[TOC]



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

  ```
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

  ```nlo
  ???? 12/4/18
  ? models with alternative non-negative distributions, not lognormal N-563 in NLOGIT 6 ref guide
  
  sample; 2-7057 $
  
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
