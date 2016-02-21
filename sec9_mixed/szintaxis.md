# Az *lme4* csomag szintaxisa 



Az *lme4* csomag az R hagyományos `formula`-jat egészíti ki azzal, hogy a 
random hatásokat `()`-ben kell megadnunk, `|` jellel elválasztva a random
hatás struktúráját magától a random faktortól.


- konstans + random konstans:

```r
library(lme4)
mod0 <- lmer(scRT ~ 1 + (1 | Subject), data = lexdec_corr)
summary(mod0)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: scRT ~ 1 + (1 | Subject)
##    Data: lexdec_corr
## 
## REML criterion at convergence: 4445.4
## 
## Scaled residuals: 
##      Min       1Q   Median       3Q      Max 
## -2.04651 -0.87606  0.09449  0.62459  2.81604 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  Subject  (Intercept) 0.08002  0.2829  
##  Residual             0.92559  0.9621  
## Number of obs: 1594, groups:  Subject, 21
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept) 0.001177   0.066272   0.018
```

- "valódi" fix hatás + random konstans + random slope:

```r
mod_trial <- lmer(scRT ~ scTrial + (1 + scTrial | Subject), 
                  data = lexdec_corr)
summary(mod_trial)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: scRT ~ scTrial + (1 + scTrial | Subject)
##    Data: lexdec_corr
## 
## REML criterion at convergence: 4446.9
## 
## Scaled residuals: 
##      Min       1Q   Median       3Q      Max 
## -2.03659 -0.88192  0.09215  0.62026  2.99275 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev. Corr 
##  Subject  (Intercept) 0.080383 0.28352       
##           scTrial     0.007607 0.08722  -0.46
##  Residual             0.918889 0.95859       
## Number of obs: 1594, groups:  Subject, 21
## 
## Fixed effects:
##               Estimate Std. Error t value
## (Intercept)  0.0003167  0.0663791   0.005
## scTrial     -0.0098790  0.0307164  -0.322
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial -0.265
```

- keresztezett random hatások:

```r
mod_crossed <- lmer(scRT ~ scTrial + (1 + scTrial | Subject) + (1 | Word), 
                    data = lexdec_corr)
summary(mod_crossed)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: scRT ~ scTrial + (1 + scTrial | Subject) + (1 | Word)
##    Data: lexdec_corr
## 
## REML criterion at convergence: 1532
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.5732 -0.6247 -0.1150  0.4565  5.9812 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev. Corr 
##  Word     (Intercept) 0.804171 0.89676       
##  Subject  (Intercept) 0.088618 0.29769       
##           scTrial     0.003924 0.06264  -0.28
##  Residual             0.111259 0.33356       
## Number of obs: 1594, groups:  Word, 79; Subject, 21
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept)  0.01238    0.12029   0.103
## scTrial     -0.01907    0.01613  -1.182
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial -0.130
```

- beágyazott random hatások (többféle megadási mód lehetséges):

```r
mod_nested1 <- lmer(scRT ~ scTrial + (1 | Page) + (1 | Word), 
                    data = lexdec_corr)
mod_nested2 <- lmer(scRT ~ scTrial + (1 | Page) + (1 | Word:Page), 
                    data = lexdec_corr)
mod_nested3 <- lmer(scRT ~ scTrial + (1 | Page/Word), 
                    data = lexdec_corr)
summary(mod_nested1)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: scRT ~ scTrial + (1 | Page) + (1 | Word)
##    Data: lexdec_corr
## 
## REML criterion at convergence: 2109.7
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.2322 -0.6717 -0.1452  0.4796  4.4835 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  Word     (Intercept) 0.0184   0.1357  
##  Page     (Intercept) 0.8515   0.9228  
##  Residual             0.2011   0.4484  
## Number of obs: 1594, groups:  Word, 79; Page, 10
## 
## Fixed effects:
##              Estimate Std. Error t value
## (Intercept)  0.003373   0.292426   0.012
## scTrial     -0.021736   0.011379  -1.910
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial 0.000
```

```r
summary(mod_nested2)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: scRT ~ scTrial + (1 | Page) + (1 | Word:Page)
##    Data: lexdec_corr
## 
## REML criterion at convergence: 2109.7
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.2322 -0.6717 -0.1452  0.4796  4.4835 
## 
## Random effects:
##  Groups    Name        Variance Std.Dev.
##  Word:Page (Intercept) 0.0184   0.1357  
##  Page      (Intercept) 0.8515   0.9228  
##  Residual              0.2011   0.4484  
## Number of obs: 1594, groups:  Word:Page, 79; Page, 10
## 
## Fixed effects:
##              Estimate Std. Error t value
## (Intercept)  0.003373   0.292426   0.012
## scTrial     -0.021736   0.011379  -1.910
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial 0.000
```

```r
summary(mod_nested3)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: scRT ~ scTrial + (1 | Page/Word)
##    Data: lexdec_corr
## 
## REML criterion at convergence: 2109.7
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.2322 -0.6717 -0.1452  0.4796  4.4835 
## 
## Random effects:
##  Groups    Name        Variance Std.Dev.
##  Word:Page (Intercept) 0.0184   0.1357  
##  Page      (Intercept) 0.8515   0.9228  
##  Residual              0.2011   0.4484  
## Number of obs: 1594, groups:  Word:Page, 79; Page, 10
## 
## Fixed effects:
##              Estimate Std. Error t value
## (Intercept)  0.003373   0.292426   0.012
## scTrial     -0.021736   0.011379  -1.910
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial 0.000
```
