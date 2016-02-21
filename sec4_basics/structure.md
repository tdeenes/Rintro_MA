# Objektumok megtekintése

Fontos tudatosítani, hogy a `print` eredménye többnyire nem felel meg az adott
objektum pontos tartalmának:


```r
options(digits = 2) # hány tizedesjegyet jelenítsen meg
vec <- rnorm(4)
print(vec)
```

```
## [1] -1.283 -1.676  0.039 -1.418
```

```r
# demonstráció 1
options(digits = 10)
vec
```

```
## [1] -1.28308651594 -1.67576263829  0.03941781855 -1.41789374301
```

```r
# demonstráció 2
class(vec) <- "specialVector"
print.specialVector <- function(x, ...) print.default("hello")
print(vec)
```

```
## [1] "hello"
```

```r
# állítsuk vissza az alapbeállításra
options(digits = 7)
```


Egy objektum struktúrájáról többet megtudhatsz az RStudio "Environment" ablakában
a megfelelő objektumra pillantva, amely valójában a `str` függvény eredményét 
jeleníti meg.

- `str` -> roppant hasznos

```r
# az előbbi példát folytatva:
str(vec)
```

```
## Class 'specialVector'  num [1:4] -1.2831 -1.6758 0.0394 -1.4179
```

```r
# új példa:
mydat <- matrix(rnorm(10), 2, 5, 
                dimnames=list(c("lower", "upper"),
                              paste("col", 1:5, sep=".")))
mydat
```

```
##           col.1      col.2      col.3      col.4       col.5
## lower -2.226631  0.4796836 -1.9032087 -0.7639304 -1.37472749
## upper -1.254593 -0.9861970 -0.9623902  1.4283198 -0.06939568
```

```r
str(mydat)
```

```
##  num [1:2, 1:5] -2.227 -1.255 0.48 -0.986 -1.903 ...
##  - attr(*, "dimnames")=List of 2
##   ..$ : chr [1:2] "lower" "upper"
##   ..$ : chr [1:5] "col.1" "col.2" "col.3" "col.4" ...
```

- hosszú listák megtekintésekor érdemes lehet használni a `str` függvény 
argumentumait (lásd `?str`)

```r
# generáljunk egy bonyolult listát 
# (illesszünk egy regressziós modellt)
fit <- lm(mpg ~ wt, mtcars)

# nézzük meg a 'fit' objektum struktúráját
str(fit, max.level = 1, give.attr = FALSE)
```

```
## List of 12
##  $ coefficients : Named num [1:2] 37.29 -5.34
##  $ residuals    : Named num [1:32] -2.28 -0.92 -2.09 1.3 -0.2 ...
##  $ effects      : Named num [1:32] -113.65 -29.116 -1.661 1.631 0.111 ...
##  $ rank         : int 2
##  $ fitted.values: Named num [1:32] 23.3 21.9 24.9 20.1 18.9 ...
##  $ assign       : int [1:2] 0 1
##  $ qr           :List of 5
##  $ df.residual  : int 30
##  $ xlevels      : Named list()
##  $ call         : language lm(formula = mpg ~ wt, data = mtcars)
##  $ terms        :Classes 'terms', 'formula' length 3 mpg ~ wt
##  $ model        :'data.frame':	32 obs. of  2 variables:
```



- `head` és `tail` -> főként data.frame esetén jön jól

```r
datfr <- data.frame(characters = letters[1:20], numbers = 1:20)
```
- első 10 elem kiírása

```r
head(datfr, 10)
```

```
##    characters numbers
## 1           a       1
## 2           b       2
## 3           c       3
## 4           d       4
## 5           e       5
## 6           f       6
## 7           g       7
## 8           h       8
## 9           i       9
## 10          j      10
```

- utolsó 10 elem kiírása

```r
tail(datfr, 10)
```

```
##    characters numbers
## 11          k      11
## 12          l      12
## 13          m      13
## 14          n      14
## 15          o      15
## 16          p      16
## 17          q      17
## 18          r      18
## 19          s      19
## 20          t      20
```
