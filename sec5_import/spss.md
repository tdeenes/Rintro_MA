# SPSS és Excel fájl beolvasása

### SPSS

SPSS fájlok beolvasásához használd a *foreign* csomagot, vagy ha az 
valamilyen okból nem működik, az újabb *haven* csomagot. (A *haven* csomaggal
akár létre is hozhatsz .sav fájlt.)


```r
library(foreign)
dat_spss <- read.spss(file.path("data", "AlkVizsg.sav"),
                      to.data.frame = TRUE)
```

```
## re-encoding from CP1250
```

```r
str(dat_spss, list.len = 5L)
```

```
## 'data.frame':	101 obs. of  34 variables:
##  $ id       : num  66 60 16 42 74 65 26 58 77 1 ...
##  $ nem      : num  2 1 2 1 2 1 2 2 2 2 ...
##  $ munkakor : Factor w/ 2 levels "gépkezelő","gépbeállító": 1 1 1 1 1 1 1 1 1 1 ...
##  $ vegz     : Factor w/ 3 levels "8 általános",..: 2 1 2 2 1 3 1 3 2 3 ...
##  $ szul_ev  : num  1965 1979 1960 1981 1961 ...
##   [list output truncated]
##  - attr(*, "variable.labels")= Named chr  "" "" "munkakör" "végzettség" ...
##   ..- attr(*, "names")= chr  "id" "nem" "munkakor" "vegz" ...
##  - attr(*, "codepage")= int 1250
```

### Excel

Az R-ben számos csomag képes Excel-fájlt beolvasni vagy készíteni. Egy
összefoglaló táblázat a leginkább releváns lehetőségekről:

Csomag | Olvasás | Írás | .xls | .xlsx | Gyors?
-------|---------|------|------|-------|------------
XLConnect | + | + | + | + | -
xlsx | + | + | + | + | -
readxl | + | - | + | + | +
openxlsx | + | + | - | + | +

Ha jól formázott Excel-táblázatod van, akkor a *readxl* csomaggal jársz a 
legjobban, ha csupán beolvasni szeretnél. Az *openxlsx* csomag hasonlóan jó
.xlsx fájlok beolvasásához, és ezzel a csomaggal készíthetsz is xlsx fájlt. 
Az *XLConnect* és *xlsx* csomagok igen rugalmasak, és jellemzően gazdagabb
funkcionalitásúak. Jelentős hátrányuk viszont, hogy Java-könyvtárra épülnek,
így egyrészt sok rendszeren a telepítésük nehézkes lehet, illetve nagyméretű
fájlok beolvasására gyakorlatilag alkalmatlanok.

### Tipp

Noha az R képes SPSS és Excel fájlok beolvasására, sokszor jobban jársz, ha
az adataidat az SPSS-ben vagy Excel-ben megnyitod, majd exportálod .csv 
formátumba.
