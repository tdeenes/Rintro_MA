# R objektumok (de)szerializációja

A szerializáció, illetve deszerializáció a memóriában tárolt objektumok külső
tárolóra történő mentését, illetve az onnan történő visszaállítást jelenti.
Közérthetőbben most arról lesz szó, hogyan lehet a legegyszerűbben elmentened,
illetve betöltened R-objektumokat.

### Mentés

- hozzunk létre két példa-adatot:

```r
x <- c(1, 3, 5, 7)
y <- data.frame(id = c("001", "002", "003"), IQ = c(92, 128, 101))
```

- egy objektum mentése:

```r
saveRDS(y, file = "iq.rds")
```

- több objektum mentése:

```r
save(x, y, file = "iq.RData")
```

- (majdnem) minden objektum mentése

```r
save(list = ls(), file = "all.RData")
```

### Visszaállítás

- a `saveRDS`-sel elmentett objektum nem tartalmazza az objektum nevét, tehát
a beolvasott adatot hozzá kell rendelnünk egy új változóhoz:

```r
y_import <- readRDS("iq.rds")

# ellenőrzés
identical(y, y_import)
```

```
## [1] TRUE
```

- a `save` parancs az objektumot és az objektum nevét is elmenti, így
betöltéskor azok is betöltődnek -> NAGYON ÓVATOS legyél, mert észrevétlenül
felülírhatsz egy memóriában tárolt változót

```r
# létrehozok egy új x változót
x <- "proba"

# betöltöm az "all.RData" fájlt
load("all.RData")

# mivel az "all.RData" fájl tartalmaz egy `x` objektumot, a betöltésével 
# felülírtuk a memóriában tárolt `x`-et
x
```

```
## [1] 1 3 5 7
```

- a `load` fentebbi kellemetlen mellékhatása kiküszöbölhető, ha egy külön
környezetbe töltjük be az adatokat, vagy ha csak beillesztjük a keresési útba

```r
# új környezet
e <- new.env(parent = emptyenv())
load("all.RData", e)
ls(e)
```

```
##  [1] "arr"                 "count"               "createSequence"     
##  [4] "createSequence2"     "dat"                 "datfr"              
##  [7] "datfr_nofactor"      "dat_num"             "estimated_means"    
## [10] "fac"                 "final_dat"           "fit"                
## [13] "fit_summary"         "gg"                  "groups"             
## [16] "i"                   "index"               "itemek"             
## [19] "likert_valtozok"     "lt"                  "marginal_means"     
## [22] "mat"                 "mat1"                "mat2"               
## [25] "mat3"                "model"               "model_dat"          
## [28] "model_dat_long"      "MOGQ_social"         "MOGQ_social_itemek" 
## [31] "mydat"               "mylist"              "my_sequence"        
## [34] "n"                   "newfac"              "nice_table"         
## [37] "packs"               "plotAnova"           "plot_dat"           
## [40] "pred_means"          "pred_table"          "pred_tables"        
## [43] "print.specialVector" "results"             "runAnova"           
## [46] "skala"               "skala_definiciok"    "skala_nevek"        
## [49] "skalapontok"         "temporary"           "vec"                
## [52] "vec_char"            "vec_down"            "vec_int"            
## [55] "vec_logic"           "vec_num"             "vec.reference"      
## [58] "vec.target"          "vec_up"              "x"                  
## [61] "y"
```

```r
# keresési út módosítása
attach("all.RData")
```

```
## The following objects are masked from file:all.RData (pos = 6):
## 
##     arr, count, createSequence, createSequence2, dat, datfr,
##     datfr_nofactor, dat_num, estimated_means, fac, final_dat, fit,
##     fit_summary, gg, groups, i, index, itemek, likert_valtozok,
##     lt, marginal_means, mat, mat1, mat2, mat3, model, model_dat,
##     model_dat_long, MOGQ_social, MOGQ_social_itemek, mydat,
##     mylist, my_sequence, n, newfac, nice_table, packs, plotAnova,
##     plot_dat, pred_means, pred_table, pred_tables,
##     print.specialVector, results, runAnova, skala,
##     skala_definiciok, skala_nevek, skalapontok, temporary, vec,
##     vec_char, vec_down, vec_int, vec_logic, vec_num,
##     vec.reference, vec.target, vec_up, x, y
```

```r
x
```

```
## [1] 1 3 5 7
```

```r
get("x", pos = 2)
```

```
## [1] 1 3 5 7
```



### Példaadatok betöltése

Számos R csomag tartalmaz "beépített" példaadatokat. Ezen adatok valójában 
.RData vagy .rda kiterjesztésű fájlok, amelyek akár egy egyszerű `load()`
paranccsal is betölthetők. Ehhez azonban tudunk kell a fájl elérési útját, ami
helyett sokkal kényelmesebb a `data()` függvényt alkalmazni. A `data()` 
először a betöltött csomagokban keresi az adott nevű adatot, majd a 
munkakönyvtár "data" nevű mappájában (már ha létezik ilyen nevű könyvtár).
A későbbiekben a `data()` parancsot gyakran fogjuk használni a példákban,
például így:


```r
# a diszlexia-vizsgálati adatok betöltése
data(dyslex)
```

