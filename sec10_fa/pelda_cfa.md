# Konfirmatív faktorelemzés 




A pszichológiai tanulmányokban gyakorta előfordul, hogy a szerzők az exploratív 
faktorelemzés eredményeit úgy értelmezik, mintha az konfirmatív faktorelemzésből
származna. Az előző példában például csábító azt feltételezni, hogy az 
ötfaktoros modellünk alátámasztja kérdőív vélt struktúráját: az itemekre kapott
válaszok egy-egy látens faktor manifesztumai, amely látens faktorok alapvetően
függetlenek egymástól, kivéve a csekély együttjárást mutató A és E faktorokat.

Valóban ilyen tiszta és egyértelmű lenne a kérdőív struktúrája? Technikailag: a kereszttöltéseket (pl. egy A faktorhoz tartozó item kapcsolatát a többi faktorral) 0-nak vehetjük, csakúgy, mint a látens faktorok kovarianciáját (kivéve az A és E faktort)? Válaszoljuk meg ezt a kérdést egy konfirmatív faktormodell
illesztésével. 

- töltsük be a *lavaan* csomagot:
    
    ```r
    library(lavaan)
    ```
    
    ```
    ## This is lavaan 0.5-20
    ```
    
    ```
    ## lavaan is BETA software! Please report any bugs.
    ```

- adjuk meg a feltételezett modell struktúráját:
    
    ```r
    model_syntax <- "
    Agreeableness =~ A1 + A2 + A3 + A4 + A5
    Conscientiousness =~ C1 + C2 + C3 + C4 + C5
    EmotionalStability =~ E1 + E2 + E3 + E4 + E5
    Extraversion =~ N1 + N2 + N3 + N4 + N5
    Openness =~ O1 + O2 + O3 + O4 + O5
       
    Agreeableness ~~ EmotionalStability
    "
    ```

- illesszük a modellt:
    
    ```r
    cfa_res <- cfa(model_syntax, data = dat,
               std.lv = TRUE, orthogonal = TRUE, missing = "fiml")
    ```

- vizsgáljuk meg az eredményeket:

```r
## ha csak kiprintelni szeretnénk az eredményeket:
#summary(cfa_res, fit.measures = TRUE)

# ha a becsült paramétereket akarjuk kinyerni
# egy data.frame-be (csak az első 10 sort jelenítjük meg):
cfa_std <- standardizedSolution(cfa_res)
head(cfa_std, 10)
```

```
##                  lhs op rhs est.std    se      z pvalue
## 1      Agreeableness =~  A1   0.332 0.020 16.951      0
## 2      Agreeableness =~  A2   0.635 0.015 43.236      0
## 3      Agreeableness =~  A3   0.744 0.013 59.024      0
## 4      Agreeableness =~  A4   0.478 0.017 27.660      0
## 5      Agreeableness =~  A5   0.682 0.014 49.136      0
## 6  Conscientiousness =~  C1   0.545 0.018 30.513      0
## 7  Conscientiousness =~  C2   0.609 0.017 35.894      0
## 8  Conscientiousness =~  C3   0.551 0.017 31.770      0
## 9  Conscientiousness =~  C4   0.669 0.016 41.612      0
## 10 Conscientiousness =~  C5   0.586 0.017 34.055      0
```

```r
# ha a modell illeszkedésére vagyunk kíváncsiak:
fitMeasures(cfa_res)
```

```
##                npar                fmin               chisq 
##              76.000               0.978            5477.743 
##                  df              pvalue      baseline.chisq 
##             274.000               0.000           20010.482 
##         baseline.df     baseline.pvalue                 cfi 
##             300.000               0.000               0.736 
##                 tli                nnfi                 rfi 
##               0.711               0.711               0.700 
##                 nfi                pnfi                 ifi 
##               0.726               0.663               0.736 
##                 rni                logl   unrestricted.logl 
##               0.736         -114680.118         -111941.247 
##                 aic                 bic              ntotal 
##          229512.237          229963.477            2800.000 
##                bic2               rmsea      rmsea.ci.lower 
##          229722.000               0.082               0.080 
##      rmsea.ci.upper        rmsea.pvalue                 rmr 
##               0.084               0.000               0.230 
##          rmr_nomean                srmr        srmr_bentler 
##               0.238               0.112               0.112 
## srmr_bentler_nomean         srmr_bollen  srmr_bollen_nomean 
##               0.116               0.112               0.116 
##          srmr_mplus   srmr_mplus_nomean               cn_05 
##               0.112               0.116             161.304 
##               cn_01                 gfi                agfi 
##             170.388               0.981               0.975 
##                pgfi                 mfi                ecvi 
##               0.768               0.395                  NA
```

A lavaan az általánosan használt illeszkedési mutatószámok mindegyikét 
feltünteti. Ezek jelentését és elvárt értékét remekül összefoglalja [ez az oldal](http://davidakenny.net/cm/fit.htm). A modell illeszkedésének mutatószámai esetünkben egyöntetűen azt jelzik, hogy a modellünk nem írja le megfelelően a változók kapcsolati mintázatát. A tanulság tehát az, hogy az exploratív
faktorelemzést tekintsük annak, ami: egy feltáró jellegű vizsgálatnak, amely
nem alkalmas különböző elméleti modellek egzakt tesztelésére.


