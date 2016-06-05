# Átstrukturálás

Az adatbevitelnél gyakran "wide" formátumban rögzítik az adatokat,
a modellezésnél viszont a "long" formátum a kedvezőbb. 

- példa wide formátumra

```r
# adatok betöltése
data(dyslex)

# első néhány sor
head(dyslex)
```

```
##   id nem csoport oszt kor figyzavar szokincs olv_helyes1 olv_helyes2
## 1 s1   1       0    3 117        50       32          28          17
## 2 s2   1       0    3 115        63       49          41          29
## 3 s3   1       0    2 108        51       20          34          35
## 4 s4   1       0    3 117        69       35          26          18
## 5 s5   1       0    3 123        53       31          28          21
## 6 s6   1       0    3 115        60       30          40          38
##   olv_helyes3 sp_helyes1 sp_helyes2 sp_helyes3 sp_helyes4 sp_helyes5
## 1          18         28         20         19         17         19
## 2          23         29         17         18         17         19
## 3          26         19         14         12         12          9
## 4          19         20         14         11         12         12
## 5          21         16          5         17         14         13
## 6          36         26         14         20         18         13
```

- elemezzük csak az olvasást

```r
dyslex_read <- subset(dyslex, 
                      select = -(sp_helyes1:sp_helyes5))
head(dyslex_read)
```

```
##   id nem csoport oszt kor figyzavar szokincs olv_helyes1 olv_helyes2
## 1 s1   1       0    3 117        50       32          28          17
## 2 s2   1       0    3 115        63       49          41          29
## 3 s3   1       0    2 108        51       20          34          35
## 4 s4   1       0    3 117        69       35          26          18
## 5 s5   1       0    3 123        53       31          28          21
## 6 s6   1       0    3 115        60       30          40          38
##   olv_helyes3
## 1          18
## 2          23
## 3          26
## 4          19
## 5          21
## 6          36
```

- alakítsuk át long formátumba (legyen egy 'blokk' és egy 'olv_helyes' változónk)

```r
dyslex_read_long <- reshape(dyslex_read, 
                            varying = c("olv_helyes1", "olv_helyes2", "olv_helyes3"),
                            timevar = "blokk",
                            v.names = "olv_helyes",
                            direction = "long")
head(dyslex_read_long)
```

```
##      id nem csoport oszt kor figyzavar szokincs blokk olv_helyes
## s1.1 s1   1       0    3 117        50       32     1         28
## s2.1 s2   1       0    3 115        63       49     1         41
## s3.1 s3   1       0    2 108        51       20     1         34
## s4.1 s4   1       0    3 117        69       35     1         26
## s5.1 s5   1       0    3 123        53       31     1         28
## s6.1 s6   1       0    3 115        60       30     1         40
```

- a *reshape2* csomaggal egyszerűbb

```r
library(reshape2)
dyslex_read_long2 <- melt(
    dyslex_read, 
    measure.vars = c("olv_helyes1", "olv_helyes2", "olv_helyes3"),
    variable.name = "mutato",
    value.name = "ertek")
```


- talán még egyszerűbb a *tidyr* csomaggal

```r
library(tidyr)
dyslex_read_long3 <- gather(dyslex_read, mutato, ertek, 
                            olv_helyes1:olv_helyes3)
```

- és szintén kellemes (és nagyon gyors) a *data.table* megoldása

```r
library(data.table)
dyslex_read_long4 <- melt(data.table(dyslex_read), 
     measure.vars = c("olv_helyes1", "olv_helyes2", "olv_helyes3"),
     variable.name = "mutato",
     value.name = "ertek")
```

- long-ból wide formátumba:
    - base: `reshape(..., direction = "wide")`
    - reshape2, data.table: `?dcast`
    - tidyr: `spread`

```r
# tidyr
dyslex_orig <- spread(dyslex_read_long3, mutato, ertek)
str(dyslex_orig)
```

```
## 'data.frame':	101 obs. of  10 variables:
##  $ id         : chr  "s1" "s10" "s100" "s101" ...
##  $ nem        : num  1 2 2 1 2 1 2 1 2 2 ...
##  $ csoport    : num  0 0 1 1 0 0 0 0 0 0 ...
##  $ oszt       : num  3 3 2 3 3 3 2 2 2 2 ...
##  $ kor        : num  117 107 118 117 107 113 96 98 102 101 ...
##  $ figyzavar  : num  50 50 54 50 54 54 50 60 50 67 ...
##  $ szokincs   : num  32 32 19 38 29 46 32 48 39 42 ...
##  $ olv_helyes1: num  28 17 44 40 33 43 28 28 21 33 ...
##  $ olv_helyes2: num  17 16 30 34 30 28 25 24 14 27 ...
##  $ olv_helyes3: num  18 16 28 37 28 31 24 17 13 23 ...
```

