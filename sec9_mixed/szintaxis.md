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
## REML criterion at convergence: 4341.3
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.2510 -0.7751  0.0437  0.6348  3.2703 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  Subject  (Intercept) 0.1506   0.3881  
##  Residual             0.8601   0.9274  
## Number of obs: 1594, groups:  Subject, 21
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept) 0.001656   0.087818   0.019
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
## REML criterion at convergence: 4339.8
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.3311 -0.7852  0.0355  0.6339  3.2934 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev. Corr 
##  Subject  (Intercept) 0.15117  0.3888        
##           scTrial     0.01051  0.1025   -0.42
##  Residual             0.85046  0.9222        
## Number of obs: 1594, groups:  Subject, 21
## 
## Fixed effects:
##              Estimate Std. Error t value
## (Intercept)  0.000863   0.087945   0.010
## scTrial     -0.016743   0.032237  -0.519
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial -0.278
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
## REML criterion at convergence: 2392.1
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.5557 -0.6257 -0.1178  0.4576  5.9873 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev. Corr 
##  Word     (Intercept) 0.651037 0.80687       
##  Subject  (Intercept) 0.158035 0.39754       
##           scTrial     0.007012 0.08373  -0.28
##  Residual             0.198417 0.44544       
## Number of obs: 1594, groups:  Word, 79; Subject, 21
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept)  0.01479    0.12606   0.117
## scTrial     -0.02541    0.02156  -1.179
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial -0.166
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
## REML criterion at convergence: 3023.3
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.2345 -0.6706 -0.1461  0.4792  4.4816 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  Word     (Intercept) 0.03282  0.1812  
##  Page     (Intercept) 0.66400  0.8149  
##  Residual             0.35859  0.5988  
## Number of obs: 1594, groups:  Word, 79; Page, 10
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept)  0.00584    0.25893   0.023
## scTrial     -0.02902    0.01520  -1.910
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
## REML criterion at convergence: 3023.3
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.2345 -0.6706 -0.1461  0.4792  4.4816 
## 
## Random effects:
##  Groups    Name        Variance Std.Dev.
##  Word:Page (Intercept) 0.03282  0.1812  
##  Page      (Intercept) 0.66400  0.8149  
##  Residual              0.35859  0.5988  
## Number of obs: 1594, groups:  Word:Page, 79; Page, 10
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept)  0.00584    0.25893   0.023
## scTrial     -0.02902    0.01520  -1.910
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
## REML criterion at convergence: 3023.3
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.2345 -0.6706 -0.1461  0.4792  4.4816 
## 
## Random effects:
##  Groups    Name        Variance Std.Dev.
##  Word:Page (Intercept) 0.03282  0.1812  
##  Page      (Intercept) 0.66400  0.8149  
##  Residual              0.35859  0.5988  
## Number of obs: 1594, groups:  Word:Page, 79; Page, 10
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept)  0.00584    0.25893   0.023
## scTrial     -0.02902    0.01520  -1.910
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial 0.000
```
