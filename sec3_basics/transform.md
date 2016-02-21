# Objektumosztályok közötti váltás

Az R-ben valamennyi alapértelmezett objektumosztályhoz tartozik olyan 
függvény, amellyel lekérdezhető, hogy az objektum az adott osztályba 
tartozik-e, illetve olyan függvény, amely az objektumot az adott 
osztályúvá alakítja. Ezen függvények általános alakja `is.something` és 
`as.something`, ahol a `something` helyére értelemszerűen az adott 
alaposztályt kell behelyettesíteni.

Példa: hozzunk létre egy-egy vektort, mátrixot, listát, és data.frame-et:

```r
( vec <- 1:4 )
```

```
## [1] 1 2 3 4
```

```r
( mat <- matrix(1:4, 2, 2) )
```

```
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
```

```r
( lt <- list(x = 1:3, y = letters[1:3]) )
```

```
## $x
## [1] 1 2 3
## 
## $y
## [1] "a" "b" "c"
```

```r
( datfr <- data.frame(x = 1:3, y = letters[1:3]) )
```

```
##   x y
## 1 1 a
## 2 2 b
## 3 3 c
```

- gyakoroljuk a lekérdezéseket (próbáld önállóan megválaszolni az utolsó 
két lekérdezés eredményét!):

```r
is.vector(vec)
```

```
## [1] TRUE
```

```r
is.matrix(mat)
```

```
## [1] TRUE
```

```r
is.list(lt)
```

```
## [1] TRUE
```

```r
is.data.frame(datfr)
```

```
## [1] TRUE
```

```r
# vajon ennek mi lesz az eredménye?
# is.list(datfr)

# ...és ennek?
# is.vector(lt)
```

- alakítsuk át őket (az utolsó átalakítások eredményét próbáld megjósolni az
eddig tanultak alapján):

```r
as.matrix(vec)
```

```
##      [,1]
## [1,]    1
## [2,]    2
## [3,]    3
## [4,]    4
```

```r
as.vector(mat)
```

```
## [1] 1 2 3 4
```

```r
as.data.frame(lt)
```

```
##   x y
## 1 1 a
## 2 2 b
## 3 3 c
```

```r
as.list(datfr)
```

```
## $x
## [1] 1 2 3
## 
## $y
## [1] a b c
## Levels: a b c
```

```r
# vajon mi történik ennél az átalakításnál?
# as.matrix(datfr)

# ...és ennél?
# as.vector(lt)
```

- olykor előfordul, hogy egy lista elemeit szeretnénk egyetlen
vektorban tárolni; ahogy láttuk, az `as.vector` parancs erre nem 
használható -> a megoldás az `unlist`

```r
unlist(lt)
```

```
##  x1  x2  x3  y1  y2  y3 
## "1" "2" "3" "a" "b" "c"
```

- érdemes megjegyezni, hogy hasonló függvények léteznek például az adattípusok lekérdezésére és konvertálására is, pl. 
`as.logical`, `as.character`, `as.integer`, `as.factor`, ...

