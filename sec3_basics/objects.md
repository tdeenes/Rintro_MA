# Az R objektum-osztályai

Vektorokra visszavezethető objektumok a következők:
- `matrix`
- `array`
- `list`
- `data.frame`
- hiányzó értékek

Speciális objektum a NULL (lásd később).


### Mátrixok (`matrix`)
- matrix = vector két dimenzióval (column-order)

```r
( mat <- matrix(1:8, nrow = 2, ncol = 4) )
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    3    5    7
## [2,]    2    4    6    8
```

```r
dim(mat)
```

```
## [1] 2 4
```

- vektorból is létrehozható

```r
vec <- 3:6
dim(vec) <- c(2, 2)
vec
```

```
##      [,1] [,2]
## [1,]    3    5
## [2,]    4    6
```

### Többdimenziós mátrix a.k.a tömb (`array`)
- array = többdimenziós vektor

```r
# array-nel vektorral adjuk meg a dimenziókat
arr <- array(1:12, c(3, 2, 2)) 
arr
```

```
## , , 1
## 
##      [,1] [,2]
## [1,]    1    4
## [2,]    2    5
## [3,]    3    6
## 
## , , 2
## 
##      [,1] [,2]
## [1,]    7   10
## [2,]    8   11
## [3,]    9   12
```

- vektorból vagy mátrixból is létrehozható

```r
vec <- 1:12
dim(vec) <- c(3, 2, 2)
vec
```

```
## , , 1
## 
##      [,1] [,2]
## [1,]    1    4
## [2,]    2    5
## [3,]    3    6
## 
## , , 2
## 
##      [,1] [,2]
## [1,]    7   10
## [2,]    8   11
## [3,]    9   12
```

### Faktorok (`factor`)
- factor = integer vektor címkékkel, amelyet az R speciálisan kezel
- kiemelten hasznos kategoriális változók tárolására

```r
fac <- factor(c(1, 1, 2, 1), 
              levels = 1:2, 
              labels = c("male", "female"))
fac
```

```
## [1] male   male   female male  
## Levels: male female
```

```r
newfac <- factor(c("male", "male", "female", "male"))
newfac
```

```
## [1] male   male   female male  
## Levels: female male
```

### Listák (`list`)
- list = speciális vektor amelyik bármilyen más elemet tartalmazhat (vektort, array-t, listát, stb.)

```r
# szorgalmi feladat: nézz utána, mi lehet a 'letters'
( lt <- list(a = 1, b = FALSE, letters[1:5]) )
```

```
## $a
## [1] 1
## 
## $b
## [1] FALSE
## 
## [[3]]
## [1] "a" "b" "c" "d" "e"
```

### Data frame (`data.frame`)
- data frame = speciális lista, amely azonos hosszúságú vektorokból áll, és 
mátrix-os elrendezésű

```r
( datfr <- data.frame(digits = 10:6, characters = letters[1:5]) )
```

```
##   digits characters
## 1     10          a
## 2      9          b
## 3      8          c
## 4      7          d
## 5      6          e
```

- a `data.frame` parancs automatikusan faktorrá alakítja a karakter-változót, 
ami nem mindig kívánatos:

```r
# a 'str' parancsról még később lesz szó, most
# a kimenetre koncentrálj:
str(datfr)
```

```
## 'data.frame':	5 obs. of  2 variables:
##  $ digits    : int  10 9 8 7 6
##  $ characters: Factor w/ 5 levels "a","b","c","d",..: 1 2 3 4 5
```

```r
# vesd össze ezzel:
( datfr_nofactor <- data.frame(digits = 10:6, 
                               characters = letters[1:5],
                               stringsAsFactors = FALSE) )
```

```
##   digits characters
## 1     10          a
## 2      9          b
## 3      8          c
## 4      7          d
## 5      6          e
```

```r
str(datfr_nofactor)
```

```
## 'data.frame':	5 obs. of  2 variables:
##  $ digits    : int  10 9 8 7 6
##  $ characters: chr  "a" "b" "c" "d" ...
```

- ha egy data.frame változóinak hossza eltérő, az R automatikusan reciklikálja
a rövidebb változókat (amennyiben lehetséges):

```r
( datfr <- data.frame(short = 1:2, long = 1:4) )
```

```
##   short long
## 1     1    1
## 2     2    2
## 3     1    3
## 4     2    4
```

### Hiányzó értékek

- hiányzó értékek: NA (not available) vagy NaN (not a number)
- minden NaN NA, de nem minden NA NaN

```r
x <- c(1, 3, 4, NaN, 5, NA)
is.na(x)
```

```
## [1] FALSE FALSE FALSE  TRUE FALSE  TRUE
```

```r
is.nan(x)
```

```
## [1] FALSE FALSE FALSE  TRUE FALSE FALSE
```

### NULL

Az R-ben a NULL egy önálló objektum, a jelentése kb. "semmi". Kezdőként a 
listákhoz kapcsolódóan fogunk találkozni vele, lásd később. 

