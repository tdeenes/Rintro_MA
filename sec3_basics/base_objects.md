# Az R alapobjektumai

- alapobjektum: vektor
    - alaposztályok: numeric, logical, integer, complex, character, list, expression, raw (az utolsó nagyon ritkán kell)
    - a vektor csak azonos alaposztályú elemeket tartalmazhat, kivéve a list
- alap nyelvi objektum: függvény (function)
    - standard használat: function_name(argument1, argument2)
- az objektumoknak lehetnek attribútumai (`?attributes`):
    - név (`names`, `dimnames`)  
    - dimenzió (`dim`)   
    - osztály (`class`)    
    - egyedi (user-defined) attribútum

### Vektor létrehozása

- vektorokat jellemzően a `c()` függvénnyel hozunk létre (`c` mint "combine"):

```r
vec <- c(1, 3, 6, 10)
vec
```

```
## [1]  1  3  6 10
```

- néhány jellemző alaposztály:

```r
# logikai vektor
vec_logic <- c(TRUE, TRUE, FALSE, FALSE)

# egész számok (integer)
vec_int <- c(1L, 10L, 100L)

# valós számok (double)
vec_num <- c(1, 10, 100)

# karakter
vec_char <- c("a", "hello", "bello")
```

- sorozat megadása

```r
( vec_up <- 10:16 ) # ez integer, hiába nincsen utána L
```

```
## [1] 10 11 12 13 14 15 16
```

```r
( vec_down <- 16:10 )
```

```
## [1] 16 15 14 13 12 11 10
```

- vektor nevekkel

```r
( vec <- c(first = 1, second = 3, third = 6, fourth = 10) )
```

```
##  first second  third fourth 
##      1      3      6     10
```

- mi történik, ha különböző alaposztályú elemeket próbálunk meg egy vektorban tárolni?

```r
( vec <- c(1, 2, "a", "b", TRUE) )
```

```
## [1] "1"    "2"    "a"    "b"    "TRUE"
```


### Függvény létrehozása

Függvényeket a `function` paranccsal tudunk létrehozni; jellemzően így:

```r
elso_fuggvenyem <- function(arg1, arg2) {
    # ezt hívjuk a függvény "testének" (body);
    # ide írjuk azokat a parancsokat, hogy mit csináljon
    # a függvény az arg1 és arg2 argumentumokkal
    a1 <- compute_this(arg1)
    a2 <- compute_that(arg2)
    a1 + a2  # az utoljára kiértékelt sor eredményét visszaadja
}
```

A következőkben készítünk egy egyszerű függvényt, amelyet egyre komplexebbé 
teszünk. A függvénynek nincsen sok értelme (az R-ben ugyanis eleve létezik a 
`seq`, `seq.int` és `seq_len` nevű függvény hasonló célra), de illusztrációnak
megteszi.

- hozzunk létre egy függvényt, amelyik létrehoz egy `n` elemű, 1-től induló 
sorozatot; ez annyira egyszerű, hogy egy sorban elfér, így a kapcsos zárójelre 
nincs is szükség

```r
createSequence <- function(n) 1:n
```

- alakítsuk úgy a függvényt, hogy növekvő és csökkenő sorozatot is 
létrehozhassunk vele: ennek érdekében bevezetünk egy második argumentumot 
(a példában szereplő `==` jel azt jelenti: "egyenlő-e?")

```r
createSequence <- function(n, direction) {
    if (direction == "up") {  
        1:n
    } else {
        n:1
    }
}
```

- létrehozhatjuk úgy is a függvényt, hogy alapértelmezetté tesszük a növekvő
sorozatot (lásd később)

```r
createSequence2 <- function(n, direction = "up") {
    if (direction == "up") {   
        1:n
    } else {
        n:1
    }
}
```

#### Hogyan hívhatók meg a függvények?
- már eddig is ezt csináltuk (az R-ben bármit csinálunk, azt valójában függvény(ek) meghívásával tesszük), de most nézzük a sajátunkra:

```r
# ha nem adunk meg argumentumnevet, akkor a függvény 
# argumentumainak eredeti sorrendje számít
createSequence(3, "up")
```

```
## [1] 1 2 3
```

```r
# ha megadjuk az argumentum nevét, az argumentumok megadásának
# sorrendje lényegtelen
createSequence(direction = "up", n = 3)
```

```
## [1] 1 2 3
```

```r
# az argumentumként megadott érték lehet egy korábban
# létrehozott objektum is
count <- 3
createSequence(count, "up")
```

```
## [1] 1 2 3
```

```r
# ha egy argumentumnak van alapértelmezett értéke, azt
# nem muszáj megadni
createSequence2(count)
```

```
## [1] 1 2 3
```

```r
createSequence2(count, "down")
```

```
## [1] 3 2 1
```

#### Hogyan lehet tárolni a függvény visszatérési értékét?
- rendeld hozzá egy objektumhoz

```r
my_sequence <- createSequence(3, "down")
my_sequence
```

```
## [1] 3 2 1
```

- többnyire a függvény-ek outputja sokkal komplexebb

```r
# példa: lineáris regresszió egy beépített adatbázison (?mtcars)
?mtcars
fit <- lm(mpg ~ wt, data = mtcars)
fit_summary <- summary(fit)
str(fit_summary)
```

```
## List of 11
##  $ call         : language lm(formula = mpg ~ wt, data = mtcars)
##  $ terms        :Classes 'terms', 'formula' length 3 mpg ~ wt
##   .. ..- attr(*, "variables")= language list(mpg, wt)
##   .. ..- attr(*, "factors")= int [1:2, 1] 0 1
##   .. .. ..- attr(*, "dimnames")=List of 2
##   .. .. .. ..$ : chr [1:2] "mpg" "wt"
##   .. .. .. ..$ : chr "wt"
##   .. ..- attr(*, "term.labels")= chr "wt"
##   .. ..- attr(*, "order")= int 1
##   .. ..- attr(*, "intercept")= int 1
##   .. ..- attr(*, "response")= int 1
##   .. ..- attr(*, ".Environment")=<environment: 0x4a674c8> 
##   .. ..- attr(*, "predvars")= language list(mpg, wt)
##   .. ..- attr(*, "dataClasses")= Named chr [1:2] "numeric" "numeric"
##   .. .. ..- attr(*, "names")= chr [1:2] "mpg" "wt"
##  $ residuals    : Named num [1:32] -2.28 -0.92 -2.09 1.3 -0.2 ...
##   ..- attr(*, "names")= chr [1:32] "Mazda RX4" "Mazda RX4 Wag" "Datsun 710" "Hornet 4 Drive" ...
##  $ coefficients : num [1:2, 1:4] 37.285 -5.344 1.878 0.559 19.858 ...
##   ..- attr(*, "dimnames")=List of 2
##   .. ..$ : chr [1:2] "(Intercept)" "wt"
##   .. ..$ : chr [1:4] "Estimate" "Std. Error" "t value" "Pr(>|t|)"
##  $ aliased      : Named logi [1:2] FALSE FALSE
##   ..- attr(*, "names")= chr [1:2] "(Intercept)" "wt"
##  $ sigma        : num 3.05
##  $ df           : int [1:3] 2 30 2
##  $ r.squared    : num 0.753
##  $ adj.r.squared: num 0.745
##  $ fstatistic   : Named num [1:3] 91.4 1 30
##   ..- attr(*, "names")= chr [1:3] "value" "numdf" "dendf"
##  $ cov.unscaled : num [1:2, 1:2] 0.38 -0.1084 -0.1084 0.0337
##   ..- attr(*, "dimnames")=List of 2
##   .. ..$ : chr [1:2] "(Intercept)" "wt"
##   .. ..$ : chr [1:2] "(Intercept)" "wt"
##  - attr(*, "class")= chr "summary.lm"
```

### Hogyan lehet megnézni egy függvény forráskódját?

- az R nyílt forráskódú: csak gépeld be a függvény nevét, zárójel nélkül

```r
var
```

```
## function (x, y = NULL, na.rm = FALSE, use) 
## {
##     if (missing(use)) 
##         use <- if (na.rm) 
##             "na.or.complete"
##         else "everything"
##     na.method <- pmatch(use, c("all.obs", "complete.obs", "pairwise.complete.obs", 
##         "everything", "na.or.complete"))
##     if (is.na(na.method)) 
##         stop("invalid 'use' argument")
##     if (is.data.frame(x)) 
##         x <- as.matrix(x)
##     else stopifnot(is.atomic(x))
##     if (is.data.frame(y)) 
##         y <- as.matrix(y)
##     else stopifnot(is.atomic(y))
##     .Call(C_cov, x, y, na.method, FALSE)
## }
## <bytecode: 0x520bc58>
## <environment: namespace:stats>
```

- vagy nézd meg a teljes forráskódot mondjuk itt: https://github.com/wch/r-source
