# Objektumok elemeinek módosítása

Egy objektum elemeinek módosítása tulajdonképpen nem más, mint az indexálás és a hozzárendelés kombinációja. 

- példa egy mátrix oszlopának "felülírására"

```r
( mat <- matrix(1:4, 2, 2) )
```

```
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
```

```r
mat[, 2] <- c(9, 10)
mat
```

```
##      [,1] [,2]
## [1,]    1    9
## [2,]    2   10
```

- figyeljünk arra, hogy az R a módosításnál is reciklikál

```r
# készítsünk egy vektort, amelyik random sorrendben tartalmazza
# az 1-10 számokat:
( vec <- sample(10) )
```

```
##  [1]  8  6  7  1  5  9 10  2  3  4
```

```r
# cseréljük ki az első négy elemét a 100 és 200 számokra
vec[1:4] <- c(100, 200)
vec
```

```
##  [1] 100 200 100 200   5   9  10   2   3   4
```

- arra is figyeljünk, hogy az R-ben egy elemi vektor (ide sorolandó a mátrix és
a tömb is) csak egyféle típusú (pl. csak integer vagy csak karakter) elemeket 
tartalmazhat -> az R ezt "észrevétlenül" kikényszeríti!

```r
( vec <- 21:30 )
```

```
##  [1] 21 22 23 24 25 26 27 28 29 30
```

```r
typeof(vec) # lásd ?typeof
```

```
## [1] "integer"
```

```r
vec[1:4] <- 1
typeof(vec)
```

```
## [1] "double"
```

```r
vec[10] <- "30"
typeof(vec)
```

```
## [1] "character"
```

- ha egy objektum tulajdonságait meg akarjuk tartani, viszont az összes elemét
ki akarjuk cserélni, érdemes lehet a következő "fogást" alkalmazni:

```r
# hozzunk létre egy mátrixot, amelyik az 1-9
# egész számokat tartalmazza, és dimenzió-nevei
# is vannak
x <- matrix(1:9, 3, 3, 
            dimnames = list(dimA = letters[1:3], 
                            dimB = LETTERS[1:3]))

# íme:
x
```

```
##     dimB
## dimA A B C
##    a 1 4 7
##    b 2 5 8
##    c 3 6 9
```

```r
# cseréljük ki a mátrix elemeit 9 véletlen (standard 
# normál eloszlású) számmal
x[] <- rnorm(9)

# az eredmény:
x
```

```
##     dimB
## dimA          A          B           C
##    a  0.2485168 -0.4680693 -0.58942127
##    b -0.4713586 -0.3746249  0.08547086
##    c  0.5223155 -0.7728817 -0.74470173
```

```r
# vesd össze ezzel a megoldással:
( y <- rnorm(9) )
```

```
## [1] -0.80743172 -0.40539830 -1.27498114  0.92210305  0.02032543  1.74862746
## [7]  0.33034475 -0.94373785 -1.75325157
```

```r
dim(y) <- dim(x)
dimnames(y) <- dimnames(x)
y
```

```
##     dimB
## dimA          A          B          C
##    a -0.8074317 0.92210305  0.3303448
##    b -0.4053983 0.02032543 -0.9437379
##    c -1.2749811 1.74862746 -1.7532516
```

- a listák elemeinek módosítása trükkösebb tud lenni:

```r
# hozzunk létre egy egyszerű listát:
( lt <- list(a = 1:3, b = 1:2, c = 1) )
```

```
## $a
## [1] 1 2 3
## 
## $b
## [1] 1 2
## 
## $c
## [1] 1
```

```r
# cseréljük ki az első listaelemet az ábécé első három betűjére
# egyik megoldás:
lt$a <- letters[1:3]

# másik megoldás:
lt[[1]] <- letters[1:3]

# cseréljük ki a 'b' listaelemet egy logikai változóra, a 'c'
# elemet pedig az ábécé első három betűjére, mindezt egyetlen
# lépésben
lt[c("b", "c")] <- list(FALSE, letters[1:3])
```

- a lista bármelyik elemét törölhetjük, ha a NULL objektumot rendeljük hozzá:

```r
# töröljük a 'c' elemet:
lt$c <- NULL

# íme az eredmény:
lt
```

```
## $a
## [1] "a" "b" "c"
## 
## $b
## [1] FALSE
```

- a fentiek fényében találd ki, hogyan lehet módosítani egy `data.frame` 
elemeit!


