# Példa

## Az adatok bemutatása

A következőkben a *languageR* csomag `lexdec` nevű példaadatát fogjuk elemezni,
amely egy lexikális döntési feladat válaszidő-eredményeit tartalmazza. A 
*languageR* csomag telepítése után az adatokat betöltheted a szokásos `data()`
paranccsal: 


```r
data(lexdec, package = "languageR")
# bővebb infó (a languageR betöltése nélkül):
?languageR::lexdec
```

- az adatok struktúrája (csak az első 10 változót megjelenítve):

```r
str(lexdec, list.len = 10)
```

```
## 'data.frame':	1659 obs. of  30 variables:
##  $ Subject       : Factor w/ 21 levels "A1","A2","A3",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ RT            : num  6.54 5.98 6.01 6.48 6.66 ...
##  $ Trial         : int  23 27 29 30 32 33 34 38 41 42 ...
##  $ Sex           : Factor w/ 2 levels "F","M": 1 1 1 1 1 1 1 1 1 1 ...
##  $ NativeLanguage: Factor w/ 2 levels "English","Other": 1 1 1 1 1 1 1 1 1 1 ...
##  $ Correct       : Factor w/ 2 levels "correct","incorrect": 1 1 1 1 1 1 1 1 1 1 ...
##  $ PrevType      : Factor w/ 2 levels "nonword","word": 2 1 1 2 1 2 2 1 1 2 ...
##  $ PrevCorrect   : Factor w/ 2 levels "correct","incorrect": 1 1 1 1 1 1 1 1 1 1 ...
##  $ Word          : Factor w/ 79 levels "almond","ant",..: 55 47 20 58 25 12 71 69 62 1 ...
##  $ Frequency     : num  4.86 4.61 5 4.73 7.67 ...
##   [list output truncated]
```

```r
head(lexdec[, 1:10])
```

```
##   Subject       RT Trial Sex NativeLanguage Correct PrevType PrevCorrect
## 1      A1 6.535331    23   F        English correct     word     correct
## 2      A1 5.979911    27   F        English correct  nonword     correct
## 3      A1 6.014888    29   F        English correct  nonword     correct
## 4      A1 6.481539    30   F        English correct     word     correct
## 5      A1 6.663978    32   F        English correct  nonword     correct
## 6      A1 6.253474    33   F        English correct     word     correct
##         Word Frequency
## 1        owl  4.859812
## 2       mole  4.605170
## 3     cherry  4.997212
## 4       pear  4.727388
## 5        dog  7.667626
## 6 blackberry  4.060443
```

A következőkben egy kegyes csalást követünk el. Annak érdekében, hogy a példaadatunk tartalmazzon beágyazott random hatásokat is, létrehozunk egy magasabb szintű 
random hatást is, és bebiztosítjuk, hogy ez a hatás legyen jelentős.

- a példa kedvéért hozzunk létre egy új változót (Page): tegyük fel, hogy a szavakat úgy kreáltuk, hogy kiválasztottunk 10 tetszőleges oldalt egy középfokú szótárból, és kigyűjtöttük az oldalon található szavakat

```r
num_cat <- 10L
lexdec$Page <- cut(as.integer(lexdec$Word), 
                   seq(0, 80, ceiling(80/num_cat)),
                   paste0("page", 1:num_cat))

# modositsuk az RT valtozot ugy, hogy legyen hatasa a Page-nek
set.seed(1) # lasd ?set.seed
page_mean <- rnorm(num_cat, 0, 0.1)
names(page_mean) <- levels(lexdec$Page)
lexdec$RT <- lexdec$RT + page_mean[lexdec$Page]
```

## Az elemzési feladat

Tegyük fel, hogy a személy anyanyelvének (NativeLanguage [= English | Other]) és az inger szemantikai kategóriájának (Class [=animal | plant]) a válaszidőkre gyakorolt hatását szeretnénk vizsgálni. Csak a helyes válaszokat vesszük figyelembe, és a kísérlet előrehaladtával együttjáró fáradási/rátanulási hatást kontrolláljuk.


