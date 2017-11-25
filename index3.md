---
title       : Bayesian VAR Model
subtitle    : Universidad Santo Tomas
author      : Andrea Amaya, Leonardo Jamaica, Gustavo Venegas & Edwin Hernandez.
job         : 
framework   : revealjs      # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Libraries and data 


```r
library(hexView)
library(dplyr)
setwd("C:/Users/USUARIO/Downloads/2017/Econometr?a")
```

```
## Error in setwd("C:/Users/USUARIO/Downloads/2017/Econometr?a"): no es posible cambiar el directorio de trabajo
```

```r
datos <- readEViews("wgmacro.wf1", as.data.frame = T)
```

```
## Warning in readEViews("wgmacro.wf1", as.data.frame = T): Skipping boilerplate variable

## Warning in readEViews("wgmacro.wf1", as.data.frame = T): Skipping boilerplate variable
```


```r
names(datos)
```

```
##  [1] "CONSUMPTION"   "DLCONSUMPTION" "DLINCOME"      "DLINVESTMENT" 
##  [5] "INCOME"        "INVESTMENT"    "LCONSUMPTION"  "LINCOME"      
##  [9] "LINVESTMENT"   "QTR"           "P228"
```


```r
Dat1 <- datos %>% select("DLINCOME", "DLCONSUMPTION", "DLINVESTMENT")
```

---

## Package
The Package used is "bvarr"

```r
library(bvarr)
```
Goals of the package:

1. Good documentation

---

## Package
The Package used is "bvarr"

```r
library(bvarr)
```
Goals of the package:

1. Good documentation
2. Versatile

---

## Package
The Package used is "bvarr"

```r
library(bvarr)
```
Goals of the package:

1. Good documentation
2. Versatile
3. Reasonable default values

---

## Package
The Package used is "bvarr"

```r
library(bvarr)
```
Goals of the package:

1. Good documentation
2. Versatile
3. Reasonable default values
4. Robustness for bad matrices

---

## Steps:
1. Create model setup from lambdas

```r
setup <- bvar_conj_setup(Dat1, p = 2)
```

```
## Not implemented yet
```
* p = number of lags


---

## Steps:

1. Create model setup from lambdas
2. Estimate bvar conjugate model from setup

```r
model <- bvar_conj_estimate(setup, keep = 2000)
```
* Keep = Number of simulations

---

## Steps:

1. Create model setup from lambdas
2. Estimate bvar conjugate model from setup
3. Summary of model

```r
bvar_conj_summary(model)
```

```
## Number of lags, p = 2
```

```
## Number of endogeneos variables, m = 3
```

```
## Number of exogeneos variables (including constant), d = 1
```

```
## Number of parameters, k = mp + d = 7
```

```
## Initial number of observations, T_in = 92
```

```
## Number of dummy observations, T_dummy = 14
```

```
## Number of observations available for classic VAR, T = T_in - p = 90
```

```
## Posterior mean of Phi (VAR coefficients) [k = 7 x m = 3]:
```

```
##                      eq_DLINCOME eq_DLCONSUMPTION eq_DLINVESTMENT
## DLINCOME, l = 1       0.27748865       0.08283411     0.363634626
## DLCONSUMPTION, l = 1  0.06084189       0.16246923     0.196887036
## DLINVESTMENT, l = 1   0.03330551      -0.01869244     0.057912802
## DLINCOME, l = 2       0.03027940       0.09904413     0.100539299
## DLCONSUMPTION, l = 2 -0.02559793       0.06218443     0.132926171
## DLINVESTMENT, l = 2   0.01927934       0.02544238    -0.022657209
## const                 0.01174505       0.01075225     0.001025187
```

```
## Posterior nu = 95
```

```
## Number of mcmc simulations, keep = 2000
```

```
## Posterior sample mean of Phi (VAR coefficients) [k = 7 x m = 3]:
```

```
##                      eq_DLINCOME eq_DLCONSUMPTION eq_DLINVESTMENT
## DLINCOME, l = 1       0.27596892       0.08173428     0.363967670
## DLCONSUMPTION, l = 1  0.06030832       0.16259989     0.183439102
## DLINVESTMENT, l = 1   0.03337397      -0.01846001     0.061025313
## DLINCOME, l = 2       0.03057048       0.09845485     0.103536240
## DLCONSUMPTION, l = 2 -0.02422096       0.06160966     0.128465131
## DLINVESTMENT, l = 2   0.01898247       0.02558721    -0.019089477
## const                 0.01173831       0.01078828     0.001093992
```

```
## Posterior sample mean of Sigma (noise covariance matrix) [m = 3 x m = 3]:
```

```
##                   DLINCOME DLCONSUMPTION DLINVESTMENT
## DLINCOME      1.594252e-04  5.321624e-05 2.153068e-05
## DLCONSUMPTION 5.321624e-05  1.378790e-04 1.287192e-04
## DLINVESTMENT  2.153068e-05  1.287192e-04 2.487345e-03
```

```
## Posterior sample sd of Phi (VAR coefficients) [k = 7 x m = 3]:
```

```
##                      eq_DLINCOME eq_DLCONSUMPTION eq_DLINVESTMENT
## DLINCOME, l = 1       0.11062688      0.100905820      0.42483922
## DLCONSUMPTION, l = 1  0.12225787      0.113647203      0.47087837
## DLINVESTMENT, l = 1   0.02765849      0.024946893      0.10797731
## DLINCOME, l = 2       0.07870696      0.075114939      0.32272317
## DLCONSUMPTION, l = 2  0.08718473      0.082421993      0.34774299
## DLINVESTMENT, l = 2   0.02175286      0.019225091      0.08518626
## const                 0.00325049      0.003023217      0.01266579
```

```
## Posterior sample sd of Sigma (noise covariance matrix) [m = 3 x m = 3]:
```

```
##                   DLINCOME DLCONSUMPTION DLINVESTMENT
## DLINCOME      2.424734e-05  1.674040e-05 6.614136e-05
## DLCONSUMPTION 1.674040e-05  2.035054e-05 6.452287e-05
## DLINVESTMENT  6.614136e-05  6.452287e-05 3.755105e-04
```

---

## Steps:

1. Create model setup from lambdas
2. Estimate bvar conjugate model from setup
3. Summary of model

---

## Results:

![Result.1](res.png)

---

## Results:

![Result.1](res2.jpg)

---


# Thanks
### By: Andrea Amaya, Leonardo Jamaica, Gustavo Venegas & Edwin Hernandez.


