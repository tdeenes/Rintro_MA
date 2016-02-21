# Objektumok kombinálása

Előfordul, hogy egyes objektumokat össze akarunk illeszteni egyetlen,
nagyobb objektumba. 

- `c()` -> az objektumokat vektorrá alakítja, és összefűzi (listáknál figyelni!)

```r
# két mátrix elemeinek összefűzése:
c(matrix(1:4, 2, 2), matrix(1:9, 3, 3))
```

```
##  [1] 1 2 3 4 1 2 3 4 5 6 7 8 9
```

```r
# ez így egy három elemű listát eredményez:
c(list(x = 1:3, y = rnorm(2)), list(c("hi", "hello")))
```

```
## $x
## [1] 1 2 3
## 
## $y
## [1] -0.1055777 -0.9963164
## 
## [[3]]
## [1] "hi"    "hello"
```

```r
# ez viszont nem:
c(list(x = 1:3, y = rnorm(2)), c("hi", "hello"))
```

```
## $x
## [1] 1 2 3
## 
## $y
## [1] 0.354963 0.376007
## 
## [[3]]
## [1] "hi"
## 
## [[4]]
## [1] "hello"
```

- `cbind()` -> oszlopok mentén történő összeillesztés

```r
# két vektor összeillesztése egy-egy oszlopba 
# (az eredmény egy mátrix)
cbind(x = 1:3, y = 4:6)
```

```
##      x y
## [1,] 1 4
## [2,] 2 5
## [3,] 3 6
```

```r
# ha az egyik vektor rövidebb, az R reciklikálja
cbind(x = 1:2, y = 1:4)
```

```
##      x y
## [1,] 1 1
## [2,] 2 2
## [3,] 1 3
## [4,] 2 4
```

```r
# ...még akkor is, ha az elemszámok nem egymás többszörösei
cbind(x = 1:3, y = 1:4)
```

```
## Warning in cbind(x = 1:3, y = 1:4): number of rows of result is not a
## multiple of vector length (arg 1)
```

```
##      x y
## [1,] 1 1
## [2,] 2 2
## [3,] 3 3
## [4,] 1 4
```

- mátrixok abban az esetben `cbind`-olhatók, ha azonos számú sorból állnak

```r
( mat1 <- matrix(1:2, 1, 2) )  
```

```
##      [,1] [,2]
## [1,]    1    2
```

```r
( mat2 <- matrix(1:4, 2, 2) )
```

```
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
```

```r
( mat3 <- matrix(5:8, 2, 2) )
```

```
##      [,1] [,2]
## [1,]    5    7
## [2,]    6    8
```


```r
cbind(mat1, mat2)
```

```
## Error in cbind(mat1, mat2): number of rows of matrices must match (see arg 2)
```

```r
cbind(mat2, mat3)
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    3    5    7
## [2,]    2    4    6    8
```

- `rbind()` -> kombinálás sorok mentén

```r
rbind(x = 1:3, y = 4:6)
```

```
##   [,1] [,2] [,3]
## x    1    2    3
## y    4    5    6
```

- `data.frame()` -> hasonló a `cbind()`-hoz, de `data.frame`-et eredményez

```r
data.frame(x = 1:3, y = 4:6)
```

```
##   x y
## 1 1 4
## 2 2 5
## 3 3 6
```

- `abind()` -> `array`-ek kombinálására (kell hozzá az *abind* csomag)

