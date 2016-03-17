# Objektumok elemeinek elérése (indexálása)

Hogyan érhetjük el egy vektor 3. elemét, egy data.frame `x` névvel ellátott 
oszlopát? A válasz: `?Extract`.

- `[` -> megőrzi az objektum alaposztályát, több elem is elérhető
- `[[` -> főként `list` és `data.frame` objektumokra, csak egy elem elérésére
- `$` -> csak `list` és `data.frame` objektumokra, csak névvel
- `@` -> S4 objektumokra (kezdőként nem kell)
- az R-ben az elemeket elérhetjük a pozíciójuk és a nevük alapján is (már 
persze ha van nekik), illetve használhatunk logikai vektort is az elemek 
megtartására vagy kizárására


### Elemek elérése vektorból

Példa:
- hozzunk létre egy vektort, amelynek elemeit nevezzük is el

```r
( vec <- c(1, 2, 4, 6) )
```

```
## [1] 1 2 4 6
```

```r
names(vec) <- c("a", "b", "d", "f")
vec
```

```
## a b d f 
## 1 2 4 6
```

```r
# ugyanez rövidebben: 
# vec <- setNames(c(1, 2, 4, 6), c("a", "b", "d", "f"))
```

- válasszuk ki a vektor 2-4. elemeit:

```r
vec[2:4]
```

```
## b d f 
## 2 4 6
```

- válasszuk ki az összes elemet, az 1. kivételével

```r
# negatív szám indexként azt jelenti, hogy 
# 'minden, kivéve az adott sorszámú elem'
vec[-1]
```

```
## b d f 
## 2 4 6
```

- válasszuk ki a "b" nevű elemét a vektornak:

```r
vec["b"]
```

```
## b 
## 2
```

- emellett logikai vektorral is indexelhetünk: a TRUE elemek maradnak, a FALSE 
elemek kiesnek:

```r
vec[c(FALSE, TRUE, FALSE, FALSE)]
```

```
## b 
## 2
```

- a logikai indexelés lehetősége elsősorban akkor jön jól, ha bizonyos 
feltételnek megfelelő elemeket akarunk kiválasztani; pl. válasszuk ki a 
2-nél nagyobb elemeket:

```r
# mely elemek nagyobbak 2-nél?
vec > 2
```

```
##     a     b     d     f 
## FALSE FALSE  TRUE  TRUE
```

```r
# az előző sor alapján az indexelés:
vec[vec > 2]
```

```
## d f 
## 4 6
```

```r
# bővebben:
temporary <- vec > 2
vec[temporary]
```

```
## d f 
## 4 6
```

- ha semmit nem írunk a zárójelbe, visszakapjuk az összes elemet:

```r
vec[]
```

```
## a b d f 
## 1 2 4 6
```


### Elemek elérése többdimenziós vektorból

TODO! Mátrixos indexálás, több sor és oszlop elérése.

- hozzunk létre egy mátrixot:

```r
( mat <- matrix((1:8)^2, 2, 4) )
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    9   25   49
## [2,]    4   16   36   64
```

- a mátrixok esetében jellemzően egy adott sort, egy adott oszlopot, vagy
adott sor(ok) adott oszlop(ai)ban lévő elem(ek)et akarunk elérni; a módszer
ugyanaz, mint a vektornál, csak dimenziónként indexelünk:

```r
# első sor elérése
mat[1, ]
```

```
## [1]  1  9 25 49
```

```r
# második oszlop elérése
mat[, 2]
```

```
## [1]  9 16
```

```r
# vegyíthetjük is az index-típusokat:
# pl. első sor igen, második sor nem, illetve 
# minden oszlop a 3. kivételével:
mat[c(TRUE, FALSE), -3]
```

```
## [1]  1  9 49
```

- ha meg akarod őrizni a dimenziókat (programozáskor nagyon hasznos):

```r
mat[, 2, drop = FALSE]
```

```
##      [,1]
## [1,]    9
## [2,]   16
```

- mivel a mátrix csupán egy dimenziókkal ellátott vektor, továbbra is 
indexelheted vektorként; pl. az első 5 elem elérése (ügyelj arra, hogy az R oszlop-orientált):

```r
mat[1:5]
```

```
## [1]  1  4  9 16 25
```

### Lista és data.frame elemeinek elérése

- hozzunk létre egy nevekkel ellátott listát:

```r
( mylist <- list(x = 1, y = 1:2, z = 1:4) )
```

```
## $x
## [1] 1
## 
## $y
## [1] 1 2
## 
## $z
## [1] 1 2 3 4
```

- egy adott nevű elem elérésére több lehetőség is van:

```r
mylist$y
```

```
## [1] 1 2
```

```r
mylist[["y"]]
```

```
## [1] 1 2
```

- több elem együttes elérése névvel...

```r
mylist[c("x", "z")]
```

```
## $x
## [1] 1
## 
## $z
## [1] 1 2 3 4
```

- ... és numerikus indexekkel:

```r
mylist[c(1, 3)]
```

```
## $x
## [1] 1
## 
## $z
## [1] 1 2 3 4
```

- készítsünk most egy data.frame-et:

```r
( datfr <- data.frame(x = 1:4, y = letters[1:4]) )
```

```
##   x y
## 1 1 a
## 2 2 b
## 3 3 c
## 4 4 d
```

- emlékezz, hogy a data.frame a lista és a mátrix kombinációjának tekinthető
- ennek megfelelően az 'y' változó elérése háromféleképpen is történhet:

```r
datfr$y
```

```
## [1] a b c d
## Levels: a b c d
```

```r
datfr[["y"]] 
```

```
## [1] a b c d
## Levels: a b c d
```

```r
datfr[, "y"]
```

```
## [1] a b c d
## Levels: a b c d
```

### Bizonyos sorok kiválasztása `data.frame`-ből

- lássuk a korábban létrehozott data.frame-et:

```r
datfr
```

```
##   x y
## 1 1 a
## 2 2 b
## 3 3 c
## 4 4 d
```

- érjük el a második sorát (emlékezz, a data.frame mátrixként is indexelhető):

```r
datfr[2, ]
```

```
##   x y
## 2 2 b
```

- érjük el azt a sort, amelynél az 'x' változó értéke nagyobb 2-nél:

```r
# hozzunk létre egy vektort, amelyiknek az elemei TRUE vagy FALSE
# attól függően, hogy a 'datfr' objektum 'x' változója nagyobb-e 2-nél
index <- datfr$x > 2

# használjuk ezt az index vektort a megfelelő sorok kinyerésére
datfr[index, ]
```

```
##   x y
## 3 3 c
## 4 4 d
```

```r
# az 'index' vektort nem muszáj expliciten létrehozni
datfr[datfr$x > 2, ]
```

```
##   x y
## 3 3 c
## 4 4 d
```

- egy kényelmesen használható függvény `data.frame` indexelésére a `subset()`

```r
subset(datfr, x > 2)
```

```
##   x y
## 3 3 c
## 4 4 d
```

- ha egy `data.frame` változóin akarsz valamilyen műveletet végezni, de nem
akarod folyton kiírni az objektum nevét, nagyon jól jön a `with()` parancs:

```r
# egészítsük ki a datfr objektumot két újabb változóval
datfr$z <- rnorm(4)
datfr$q <- c(1, 1, -1, -1)

# mennyi az x változó átlagának és z változó q hatványának a szorzata?
with(datfr, mean(x) * z^q)
```

```
## [1]  -4.177713   2.378771 106.582710   6.624711
```

```r
# with() nélkül: mean(datfr$x) * datfr$z^datfr$q
```

