


# Szűrés és összegzés

- töltsük be a "beépített" adatot

```r
data(dyslex)
```

- válasszuk ki a 145 hónapnál fiatalabb, és legfeljebb 4. osztályos gyerekeket, 
és a helyesírási adatokat válasszuk le egy külön adattáblába

```r
dyslex_read <- subset(dyslex, 
                      kor < 145 & oszt <= 4, 
                      select = -(sp_helyes1:sp_helyes5))
dyslex_spell <- subset(dyslex, 
                       kor < 145 & oszt <= 4, 
                       select = c(id, sp_helyes1:sp_helyes5))
```

- számoljuk ki `dyslex_read` változóinak az évfolyamonkénti 
átlagpontszámait:

```r
( dyslex_means <- aggregate(dyslex_read[, -1], 
                            dyslex_read["oszt"], 
                            FUN = "mean") )
```

```
##   oszt      nem   csoport oszt      kor figyzavar szokincs olv_helyes1
## 1    2 1.483871 0.4838710    2 103.4516  59.25806 32.38710    30.80645
## 2    3 1.382979 0.4255319    3 115.5532  58.93617 34.42553    33.23404
## 3    4 1.235294 0.5294118    4 127.5882  59.94118 42.29412    35.47059
##   olv_helyes2 olv_helyes3
## 1    23.61290    21.29032
## 2    26.17021    23.53191
## 3    28.29412    24.41176
```

- nagyméretű adattáblánál a fentebbi módszerek igen lassúak lehetnek; 
a megoldás a *dplyr* vagy a *data.table* csomagok használata lehet

### dplyr


```r
# könyvtár betöltése; az üzenetből látható, hogy
# a dplyr számos olyan függvényt tartalmaz, amelynek
# neve alapfüggvények neveivel egyezik meg 
library(dplyr)

# számítás
result <- 
    tbl_df(dyslex) %>%
        filter(kor < 145 & oszt <= 4) %>%
        select(-starts_with("sp_")) %>%
        group_by(oszt) %>%
        summarize(olv1 = mean(olv_helyes1), 
                  olv2 = mean(olv_helyes2), 
                  olv3 = mean(olv_helyes3))

# a dplyr eltávolítása a keresési útról
detach(package:dplyr)
```

### data.table


```r
library(data.table)
ind <- grep("sp_", colnames(dyslex), invert = TRUE)
dyslex_dt <- data.table(dyslex)[kor < 145 & oszt <= 4, ind, with = FALSE]
dyslex_dt[, lapply(.SD, mean), .SDcols = -1, by = oszt]
```

