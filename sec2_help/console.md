



# Segítség a parancssorból (konzolból)

- a CRAN repozitóriumba csak olyan csomag kerülhet be, amely megfelelően dokumentált



### Releváns R-parancsok
- `help.start()` -> elindítja a központi keresőfelületet 
- ha bizonyos fv-ek dokumentációjára vagyunk kíváncsiak (csak a betöltött csomagokban keres):

```r
help("median") 
# roviden:
?median
```
- az összes telepített csomagban keres:

```r
help.search("harmonic mean")
# roviden: 
??"harmonic mean"
```
- egy csomag összes fv-ét megjeleníti:

```r
library(help = "lattice")
help(package = "lattice")
```
- kulcsszavakra keresés:

```r
RSiteSearch("linear mixed models")
```
- ... uez felhasználóbarátabban:

```r
library(sos) # egy csomag "betoltese"
findFn("additive mixed models")
```
- sok szerző ír vignette-t -> ezek nagyon hasznosak

```r
browseVignettes(package = "data.table")
#vignette(package = "data.table")
#vignette("datatable-faq", package = "data.table")
```

### Interaktív kurzus parancssorból

A [swirl](http://swirlstats.com/) egy olyan R-csomag, amelynek segítségével 
interaktív módon ismerkedhetsz az R-rel (kvázi egy robot-tanár). A linkelt
honlapon minden infót megtalálsz a csomag használatáról.

