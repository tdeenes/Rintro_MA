# Munkakönyvtár, fájlműveletek

Mielőtt rátérünk az adatbeolvasásra és -kiírásra, néhány praktikus infó:

1) Ne felejtkezz el a munkakönyvtár beállításáról (ez automatikusan megtörténik
akkor, ha az RStudio-ban Project-et használsz):

```r
# aktuális munkakönyvtár (=working directory)
( wd <- getwd() )
```

```
## [1] "/home/tdenes/Documents/Eloadasok/2016/ELTE_RkurzusMA/Rintro_MA/sec5_import"
```

```r
# munkakönyvtár módosítása
setwd("..")

# visszalépés az eredeti munkakönyvtárba
setwd(wd)
```

2) Az R képes egyszerű fájlműveletekre, mint például:

- egy könyvtár tartalmának megjelenítése

```r
# a (rejtett fájlok nélküli) teljes lista
dir()
```

```
##  [1] "data"          "README.md"     "serialize.md"  "serialize.Rmd"
##  [5] "spss.md"       "spss.Rmd"      "text.md"       "text.Rmd"     
##  [9] "wd.md"         "wd.Rmd"
```

```r
# bizonyos mintázatú fájlnevek
dir(pattern = "Rmd")
```

```
## [1] "serialize.Rmd" "spss.Rmd"      "text.Rmd"      "wd.Rmd"
```

```r
# a dir() és a list.files() ugyanaz
?dir
```

- fájlok másolása, törlése stb.

```r
?file.copy
```

- fájlok alapinformációinak elérése (pl. méret)

```r
?file.info
```

