# Változók átalakítása

Miután sikerült betölteni az adatokat, és megfelelő formába rendezni az 
adattáblát vagy adattáblákat, gyakran újabb feladat vár ránk: 

- egyes változók alaposztálya (típusa) nem megfelelő, ezeket módosítani kell
- a faktorváltozónk szintjei nem megfelelők, például egyes szinteket össze 
akarunk vonni, vagy az alapértelmezett szintként egy másik szintet megadni 
- egyes változókat elő kell állítani más változókból

### Típus megváltoztatása (coercion)

- minden változótípusnak (`logical`, `character`, `integer`, `numeric`, 
`double`, `factor` stb.) van egy alaposztálya, amelyre rákérdezhetünk a 
`class` függvénnyel, tesztelhetjük az `is.something` függvénnyel, és 
átalakíthatjuk az `as.something` függvénnyel

- töltsük be a korábban már bemutatott `dyslex` adattáblát:

```r
data(dyslex)
```

- nézzük meg, hogy az egyes változók milyen típusúak:

```r
str(dyslex)
```

```
## 'data.frame':	101 obs. of  15 variables:
##  $ id         : chr  "s1" "s2" "s3" "s4" ...
##  $ nem        : num  1 1 1 1 1 1 1 2 1 2 ...
##  $ csoport    : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ oszt       : num  3 3 2 3 3 3 3 3 2 3 ...
##  $ kor        : num  117 115 108 117 123 115 119 109 102 107 ...
##  $ figyzavar  : num  50 63 51 69 53 60 57 54 50 50 ...
##  $ szokincs   : num  32 49 20 35 31 30 40 36 47 32 ...
##  $ olv_helyes1: num  28 41 34 26 28 40 44 36 39 17 ...
##  $ olv_helyes2: num  17 29 35 18 21 38 40 36 30 16 ...
##  $ olv_helyes3: num  18 23 26 19 21 36 36 28 32 16 ...
##  $ sp_helyes1 : num  28 29 19 20 16 26 21 21 20 20 ...
##  $ sp_helyes2 : num  20 17 14 14 5 14 15 15 6 8 ...
##  $ sp_helyes3 : num  19 18 12 11 17 20 9 15 8 16 ...
##  $ sp_helyes4 : num  17 17 12 12 14 18 18 15 14 8 ...
##  $ sp_helyes5 : num  19 19 9 12 13 13 16 13 6 14 ...
```

- látható, hogy több változó típusa nem megfelelő, pl. az `id`, `nem` és 
`csoport` változónknak faktoroknak kellene lenniük, nem pedig karakter és 
pláne nem numerikus típusúnak

```r
# az 'id' változónál teljesen mindegy, hogy mik lesznek a faktorok szintjei
# es címkéi
dyslex$id <- as.factor(dyslex$id)

# a 'nem' változónal eldönthetjük, hogy a fiúk vagy a lányok jelentsék-e az
# alapszintet (a próba kedvéért legyenek a lányok)
dyslex$nem <- factor(dyslex$nem, levels = c(2, 1), labels = c("lany", "fiu"))

# a 'csoport' változónal a kontrollcsoportot (0-s kód) érdemes alapszintnek
# hagyni
dyslex$csoport <- factor(dyslex$csoport, levels = c(0, 1), 
                         labels = c("kontroll", "sni"))
```

### Folytonos változók faktorrá alakítása, faktorszintek módosítása

> FIGYELEM! Folytonos változókat csak nyomós érv esetén alakítsatok 
> kategoriális változóvá!

- tegyük fel, hogy a figyelemzavar skála alapján szeretnénk kialakítani 
három csoportot, mégpedig 65 pont alatt "kontroll", 65-69 pont között 
"szubklinikai", 70 pont vagy fölött pedig "adhd" címkével

```r
# lásd ?cut
dyslex$figy_csop <- cut(
    dyslex$figyzavar, 
    breaks = c(0, 64, 69, Inf), # az Inf a végtelent jelöli
    labels = c("kontroll", "szubklinikai", "adhd"),
    ordered_result = TRUE)
```

- tegyük fel, hogy ez az ADHD csoportosítás már eleve megvolt, és most úgy
döntünk, hogy a szubklinikai és ADHD-s csoportot összevonjuk

```r
# eredeti faktorszintek
levels(dyslex$figy_csop)
```

```
## [1] "kontroll"     "szubklinikai" "adhd"
```

```r
# a faktorszint módosítása
levels(dyslex$figy_csop) <- c("kontroll", "adhd", "adhd")
```

### Új változó létrehozása más változók összegeként (vagy szorzataként, átlagaként stb.)

- a legjobb a `rowSums`, `rowMeans` függvényeket használni:

```r
dyslex$olvasas <- rowSums(subset(dyslex, select = olv_helyes1:olv_helyes3))
dyslex$helyesiras <- rowSums(subset(dyslex, select = sp_helyes1:sp_helyes5))
```

