# Előkészítés 

Mielőtt hozzákezdünk bármilyen elemzéshez, tegyük meg a következőket:
1) Hozzunk létre egy külön könyvtárat, amelyben a feldolgozó/elemző R-szkripteket
tárolni szeretnénk (pl. jelen esetben a könyvtár neve lehetne "gaming").
2) Ha a feldolgozandó fájlok mérete nem túlzottan nagy, hozzunk létre egy 
alkönyvtárat az adatoknak, és másoljuk oda a szükséges adatfájlokat (pl. jelen 
esetben létrehozunk egy "data" könyvtárat, benne a "gaming_random.sav" és "gaming_valtozok.txt" fájlokkal).
3) Hozzunk létre egy új projektet az RStudio-ban: File / New project, majd a 
felnyíló ablakban válasszuk az Existing Directory opciót. A következő ablakban válasszuk ki az imént létrehozott projektkönyvtárat ("gaming"). Innentől a 'gaming'
projektet könnyedén elérhetjük a jobb fölső sarokban lévő projektválasztó 
legördülő menü segítségével. 

## Adatok beolvasása

SPSS-adatokat szeretnénk beolvasni: egy [korábbi fejezetpontban](../sec5_import/spss.html) már leírtuk, hogy ehhez használhatjuk a *foreign* csomag `read.spss()` parancsát.


```r
library(foreign)
dat <- read.spss(file.path("data", "gaming_random.sav"),
                 to.data.frame = TRUE)
```

```
## Warning in read.spss(file.path("data", "gaming_random.sav"), to.data.frame
## = TRUE): data/gaming_random.sav: Unrecognized record type 7, subtype 18
## encountered in system file
```

Ha ezt a parancsot kiadjuk, az R beolvassa az adatfájlt, de közben figyelmeztetést is küld. Vajon aggódjunk-e a figyelmeztetés miatt? Vizsgáljuk meg a beolvasott adatainkat:

```r
str(dat)
```

```
## 'data.frame':	5289 obs. of  108 variables:
##  $ Sorszam       : num  49 54 55 56 57 58 60 68 69 75 ...
##  $ Problematic   : Factor w/ 2 levels "non-disordered",..: 2 1 2 1 2 2 2 2 1 1 ...
##  $ Heavy_use     : Factor w/ 2 levels "less than or equal to 4 h/day",..: 2 2 2 2 1 1 1 1 1 2 ...
##  $ Gender        : Factor w/ 2 levels "male","female": 1 1 1 1 1 1 2 1 1 1 ...
##  $ Age           : num  19 15 20 15 31 16 14 16 27 25 ...
##  $ Relationship  : Factor w/ 6 levels "single","in a relationship, but living separately",..: 1 1 1 1 3 1 NA 1 1 1 ...
##  $ Education     : num  11 8 13 8 22 10 8 11 18 13 ...
##  $ StudyCurrently: Factor w/ 2 levels "no","yes": 2 2 2 1 2 2 2 2 1 1 ...
##  $ WorkCurrently : Factor w/ 5 levels "no","Yes, I have a full-time job",..: 1 1 5 NA 2 1 1 1 2 1 ...
##  $ WeeklyGameTime: Factor w/ 6 levels "none","less than 7 hours weekly (less than one hour a day)",..: 5 5 5 5 2 3 3 3 3 5 ...
##  $ MOGQ1         : Factor w/ 5 levels "almost never/never",..: 2 2 4 1 5 1 5 1 2 3 ...
##  $ MOGQ2         : Factor w/ 5 levels "almost never/never",..: 5 3 2 1 4 4 3 1 4 1 ...
##  $ MOGQ3         : Factor w/ 5 levels "almost never/never",..: 2 3 1 3 4 3 2 1 2 4 ...
##  $ MOGQ4         : Factor w/ 5 levels "almost never/never",..: 2 5 3 2 3 4 3 2 5 1 ...
##  $ MOGQ5         : Factor w/ 5 levels "almost never/never",..: 1 5 3 1 4 4 1 1 2 4 ...
##  $ MOGQ6         : Factor w/ 5 levels "almost never/never",..: 5 5 3 2 5 1 4 1 5 2 ...
##  $ MOGQ7         : Factor w/ 5 levels "almost never/never",..: 4 1 1 2 4 4 3 5 1 4 ...
##  $ MOGQ8         : Factor w/ 5 levels "almost never/never",..: 1 4 5 3 4 4 1 3 2 2 ...
##  $ MOGQ9         : Factor w/ 5 levels "almost never/never",..: 2 3 5 5 2 1 4 1 1 2 ...
##  $ MOGQ10        : Factor w/ 5 levels "almost never/never",..: 5 3 3 1 4 2 2 2 4 2 ...
##  $ MOGQ11        : Factor w/ 5 levels "almost never/never",..: 4 3 3 1 1 5 5 2 3 4 ...
##  $ MOGQ12        : Factor w/ 5 levels "almost never/never",..: 1 2 4 4 1 3 2 1 4 2 ...
##  $ MOGQ13        : Factor w/ 5 levels "almost never/never",..: 4 5 1 4 4 3 1 1 2 1 ...
##  $ MOGQ14        : Factor w/ 5 levels "almost never/never",..: 2 2 2 5 2 3 2 1 2 4 ...
##  $ MOGQ15        : Factor w/ 5 levels "almost never/never",..: 2 1 4 3 4 1 4 1 1 5 ...
##  $ MOGQ16        : Factor w/ 5 levels "almost never/never",..: 1 4 4 1 2 1 1 1 5 2 ...
##  $ MOGQ17        : Factor w/ 5 levels "almost never/never",..: 2 2 5 1 5 3 2 4 2 3 ...
##  $ MOGQ18        : Factor w/ 5 levels "almost never/never",..: 4 3 5 3 4 1 4 3 3 3 ...
##  $ MOGQ19        : Factor w/ 5 levels "almost never/never",..: 4 1 5 5 3 2 4 1 2 1 ...
##  $ MOGQ20        : Factor w/ 5 levels "almost never/never",..: 3 1 1 3 5 5 5 4 1 3 ...
##  $ MOGQ21        : Factor w/ 5 levels "almost never/never",..: 3 3 4 3 5 5 1 2 5 5 ...
##  $ MOGQ22        : Factor w/ 5 levels "almost never/never",..: 5 4 1 4 3 1 4 4 3 3 ...
##  $ MOGQ23        : Factor w/ 5 levels "almost never/never",..: 2 4 2 4 3 3 1 4 2 4 ...
##  $ MOGQ24        : Factor w/ 5 levels "almost never/never",..: 3 5 4 1 5 2 2 1 2 2 ...
##  $ MOGQ25        : Factor w/ 5 levels "almost never/never",..: 3 3 4 5 5 2 3 3 2 5 ...
##  $ MOGQ26        : Factor w/ 5 levels "almost never/never",..: 4 4 1 1 2 3 4 4 4 4 ...
##  $ MOGQ27        : Factor w/ 5 levels "almost never/never",..: 2 3 5 3 1 3 3 1 4 3 ...
##  $ POGQ1         : Factor w/ 5 levels "never","seldom",..: 5 3 1 2 5 3 5 5 1 3 ...
##  $ POGQ2         : Factor w/ 5 levels "never","seldom",..: 4 5 4 4 1 5 5 3 4 1 ...
##  $ POGQ3         : Factor w/ 5 levels "never","seldom",..: NA 2 1 4 NA 1 NA 1 1 1 ...
##  $ POGQ4         : Factor w/ 5 levels "never","seldom",..: 1 3 3 1 3 5 2 1 5 1 ...
##  $ POGQ5         : Factor w/ 5 levels "never","seldom",..: 4 2 2 4 5 3 2 4 1 1 ...
##  $ POGQ6         : Factor w/ 5 levels "never","seldom",..: 4 4 1 1 2 5 4 5 3 1 ...
##  $ POGQ7         : Factor w/ 5 levels "never","seldom",..: NA 2 1 5 NA 3 NA 2 2 1 ...
##  $ POGQ8         : Factor w/ 5 levels "never","seldom",..: 2 5 1 4 2 1 3 2 3 1 ...
##  $ POGQ9         : Factor w/ 5 levels "never","seldom",..: 3 2 4 4 5 3 2 4 5 2 ...
##  $ POGQ10        : Factor w/ 5 levels "never","seldom",..: 3 5 1 5 3 2 3 1 2 5 ...
##  $ POGQ11        : Factor w/ 5 levels "never","seldom",..: 1 4 1 1 5 3 3 1 5 5 ...
##  $ POGQ12        : Factor w/ 5 levels "never","seldom",..: 1 4 2 1 5 2 1 2 4 3 ...
##  $ POGQ13        : Factor w/ 5 levels "never","seldom",..: 2 3 5 4 3 4 3 1 3 3 ...
##  $ POGQ14        : Factor w/ 5 levels "never","seldom",..: NA 3 1 4 NA 1 NA 1 1 1 ...
##  $ POGQ15        : Factor w/ 5 levels "never","seldom",..: 3 2 1 3 2 3 4 2 2 1 ...
##  $ POGQ16        : Factor w/ 5 levels "never","seldom",..: 1 4 1 4 4 1 1 2 5 1 ...
##  $ POGQ17        : Factor w/ 5 levels "never","seldom",..: 2 1 4 2 1 5 5 2 5 4 ...
##  $ POGQ18        : Factor w/ 5 levels "never","seldom",..: 3 1 1 5 3 5 5 2 5 1 ...
##  $ BSI1          : Factor w/ 5 levels "not at all","a little bit",..: 3 1 5 2 2 1 2 1 1 4 ...
##  $ BSI2          : Factor w/ 5 levels "not at all","a little bit",..: 1 3 4 2 5 3 1 1 2 5 ...
##  $ BSI3          : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI4          : Factor w/ 5 levels "not at all","a little bit",..: 1 1 1 3 5 2 2 2 2 2 ...
##  $ BSI5          : Factor w/ 5 levels "not at all","a little bit",..: 4 5 5 5 1 4 4 3 3 1 ...
##  $ BSI6          : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI7          : Factor w/ 5 levels "not at all","a little bit",..: 4 2 4 2 2 4 1 5 2 4 ...
##  $ BSI8          : Factor w/ 5 levels "not at all","a little bit",..: 2 5 3 2 2 1 1 2 3 4 ...
##  $ BSI9          : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI10         : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI11         : Factor w/ 5 levels "not at all","a little bit",..: 2 3 2 1 1 4 5 5 4 4 ...
##  $ BSI12         : Factor w/ 5 levels "not at all","a little bit",..: 1 2 5 5 5 4 5 3 4 2 ...
##  $ BSI13         : Factor w/ 5 levels "not at all","a little bit",..: 1 3 1 3 1 4 3 2 2 1 ...
##  $ BSI14         : Factor w/ 5 levels "not at all","a little bit",..: 1 3 2 4 2 5 5 2 2 1 ...
##  $ BSI15         : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI16         : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI17         : Factor w/ 5 levels "not at all","a little bit",..: 2 5 3 5 5 5 1 4 1 1 ...
##  $ BSI18         : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI19         : Factor w/ 5 levels "not at all","a little bit",..: 4 2 4 1 2 5 4 1 1 5 ...
##  $ BSI20         : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI21         : Factor w/ 5 levels "not at all","a little bit",..: 3 1 4 2 1 3 4 4 4 1 ...
##  $ BSI22         : Factor w/ 5 levels "not at all","a little bit",..: 5 4 4 5 5 2 3 5 1 4 ...
##  $ BSI23         : Factor w/ 5 levels "not at all","a little bit",..: 2 1 3 3 4 5 4 3 4 3 ...
##  $ BSI24         : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI25         : Factor w/ 5 levels "not at all","a little bit",..: 3 5 1 1 5 2 3 3 3 4 ...
##  $ BSI26         : Factor w/ 5 levels "not at all","a little bit",..: 5 5 2 1 4 3 3 2 4 3 ...
##  $ BSI27         : Factor w/ 5 levels "not at all","a little bit",..: 3 5 3 5 3 3 1 3 5 1 ...
##  $ BSI28         : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI29         : Factor w/ 5 levels "not at all","a little bit",..: 1 2 5 2 4 2 3 4 1 3 ...
##  $ BSI30         : Factor w/ 5 levels "not at all","a little bit",..: 2 3 5 5 1 1 5 3 3 2 ...
##  $ BSI31         : Factor w/ 5 levels "not at all","a little bit",..: 3 1 4 3 3 2 5 4 2 1 ...
##  $ BSI32         : Factor w/ 5 levels "not at all","a little bit",..: 3 5 2 3 3 3 4 5 4 4 ...
##  $ BSI33         : Factor w/ 5 levels "not at all","a little bit",..: 5 2 3 1 4 2 2 5 3 1 ...
##  $ BSI34         : Factor w/ 5 levels "not at all","a little bit",..: 1 1 2 3 1 5 5 5 2 5 ...
##  $ BSI35         : Factor w/ 5 levels "not at all","a little bit",..: 2 5 4 4 5 4 5 2 3 1 ...
##  $ BSI36         : Factor w/ 5 levels "not at all","a little bit",..: 5 4 3 5 3 4 5 4 3 4 ...
##  $ BSI37         : Factor w/ 5 levels "not at all","a little bit",..: 5 5 1 1 2 4 5 1 1 1 ...
##  $ BSI38         : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI39         : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI40         : Factor w/ 5 levels "not at all","a little bit",..: 1 1 2 5 3 3 4 3 1 2 ...
##  $ BSI41         : Factor w/ 5 levels "not at all","a little bit",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ BSI42         : Factor w/ 5 levels "not at all","a little bit",..: 3 1 3 2 1 1 5 4 3 5 ...
##  $ BSI43         : Factor w/ 5 levels "not at all","a little bit",..: 4 2 1 2 2 3 3 2 4 4 ...
##  $ BSI44         : Factor w/ 5 levels "not at all","a little bit",..: 1 4 5 3 5 5 1 3 3 5 ...
##   [list output truncated]
##  - attr(*, "variable.labels")= Named chr  "ID number of respondents" "IGD9 2 kat DSM alapján (>=5 disordered)" "Heavy use (gaming time)" "Gender" ...
##   ..- attr(*, "names")= chr  "Sorszam" "Problematic" "Heavy_use" "Gender" ...
##  - attr(*, "codepage")= int 65001
```

```r
#head(dat)
#tail(dat)
```

A beolvasott adattábla jónéhány hiányzó értéket tartalmaz, de egyébként rendben lévőnek tűnik. Következő lépésben bármilyen internetes keresővel érdemes ellenőrizni, hogy találunk-e releváns bejegyzést ugyanezzel az üzenettel (egyszerűen másoljuk be a figyelmeztető üzenetet a keresőmezőbe). A találatokat átböngészve kiderül, hogy az üzenet miatt nem kell aggódnunk, az adatok beolvasását az "unrecognized record type 7" nem befolyásolja.

## Kérdőív-itemek mint faktorok vs egész számok

Van azonban egy valódi probléma: a 'dat' adattáblában az összes kérdőív-item
faktorként szerepel. Ez azért van így, mert a `read.spss()` függvény `use.value.labels` argumentuma alapesetben TRUE, azaz a függvény a beolvasás
során faktorrá alakít minden olyan változót, amelynek szintjeihez az SPSS-ben szöveges címkék tartoztak. Ez azért is problémás lehet, mert így például a "0" = "never", "1" = "rarely", "2" = "often", "3" = "always" kódú változókat az R olyan faktorként kódolja, amelynek a szintjei megfelelnek az SPSS címkéknek, viszont a belső, integer reprezentációja 1-től 4-ig terjed. (Ez a probléma a jelen esetben 
azért nem lényeges, mert a végén úgyis a standardizált skálapontszámokkal fogunk
dolgozni).

A továbbiakban tehát két lehetőségünk van: vagy eleve numerikus változóként olvassuk be a kérdőív-itemeket, vagy utólag konvertáljuk őket numerikussá. 

1) Kérdőív-itemek beolvasása numerikusként:
- itt kihasználjuk azt, hogy a számunkra fontos, valóban faktorként reprezentálandó változók (Heavy_use, Problematic) kétszintűek, és hogy a `read.spss()` függvénynek vagy egy `max.value.labels` argumentuma (lásd a függvény súgóját)

```r
dat_num <- read.spss(file.path("data", "gaming_random.sav"), 
                     max.value.labels = 2)
```

```
## Warning in read.spss(file.path("data", "gaming_random.sav"),
## max.value.labels = 2): data/gaming_random.sav: Unrecognized record type 7,
## subtype 18 encountered in system file
```


2) Kérdőív-itemek átalakítása numerikussá:
- Ahogy [egy korábbi fejezetben](../sec6_process/convert.html) bemutattuk, egy változót integerré alakíthatunk az `as.integer`, vagy valós számmá az `as.double` vagy `as.numeric` paranccsal, például:

```r
dat$MOGQ1 <- as.integer(dat$MOGQ1)
```

- Kézzel átírni az előző sort az összes kérdőív-item nevére igen fáradságos feladat lenne. A megoldás kézenfekvő: készítsünk egy karakter vektort, amely tartalmazza
az összes kérdéses változónevet, majd egy ciklussal menjünk végig az adattábla összes érintett oszlopán, és konvertáljuk az oszlopot a megfelelő típusra:

```r
# tudjuk, hogy a kérdőív itemek az 
# MOGQ, POGQ vagy BSI karaktereket tartalmazzák;
# akár le is ellenőrizheted: colnames(dat)
likert_valtozok <- grep("MOGQ|POGQ|BSI", 
                        colnames(dat), 
                        value = TRUE)

# meggyőződhetsz róla, hogy a likert_valtozok vektor 
# valóban a kérdéses itemeket tartalmazza
#print(likert_valtozok)

# ciklus
for (i in likert_valtozok) {
    dat[, i] <- as.integer(dat[, i])
}
```

A fentebbi sorok a következőt jelentik:

```r
for (i in likert_valtozok)
```
-> vedd a likert_valtozok vektort, és lépkedj végig az összes elemén; az aktuálisan
kiválasztott elemet jelölje `i`


```r
dat[, i] <- as.integer(dat[, i])
```
-> az `i` ciklusváltozó tartalmának megfelelő változót válaszd ki a `dat` data.frame-ből, alakítsd át egész számmá, és írd felül az eredeti változót ezekkel az értékekkel

## Skálapontszámok

A leírás alapján a kérdőívek nem tartalmaznak fordított itemeket. Ennek ellenére nem árt ellenőrizni, hogy a kérdőívek tételei valóban egy irányba mutatnak-e. A kérdőív-itemek korrelációs mátrixa remekül vizualizálható a [már ismert](../sec10_fa/pelda_efa.html) *corrplot* csomag `corrplot()` függvényével. Ezúttal olyan megjelenítést választunk, hogy az itemek a McQuitty-féle hierarchikus klaszterelemzés eredményei szerint legyenek sorba rendezve. A változók nagy száma miatt az ábrát png fájlba mentjük utólagos megtekintésre.

```r
library(corrplot)
png("corr_items.png", width = 1000, height = 1000)
corrplot(cor(dat[, likert_valtozok], use = "p"), 
         method = "square", diag = FALSE,
         order = "hclust", hclust.method = "mcquitty", 
         tl.cex = 0.7)
dev.off()
```

```
## png 
##   2
```



Mivel randomizált adatokon dolgozunk, a korrelációs eredményeink természetesen nehezen lennének interpretálhatók. Az azonban így is látszik, hogy a kérdőívekben valóban nem szerepeltek fordított itemek. A következő lépés tehát a skálapontszámok számolása. 

Ha a skálapontszámokat egyedileg szeretnénk kiszámolni, a következőt tehetnénk:
1. Készítünk egy vektort, amely tartalmazza az adott skálához tartozó itemek
nevét:

```r
MOGQ_social_itemek <- c("MOGQ1", "MOGQ8", "MOGQ15", "MOGQ22")
```

2. Kiválasztjuk az adattáblánkból a megfelelő oszlopokat, és kiszámoljuk 
ezen résztábla sorátlagait (a hiányzó értékek eltávolításával):

```r
MOGQ_social <- rowMeans(dat[, MOGQ_social_itemek],
                        na.rm = TRUE)
```

Ez egyrészt fáradságos és lassú folyamat, másrészt az itemek nevének egyedi másolgatása és/vagy begépelése miatt a hibázás valószínűsége is magas. A folyamatot két ponton tehetnénk hatékonyabbá: egyrészt megfelelő formába kellene hozni a txt-ben kapott skáladefiníciókat, másrészt automatizálni kellene a skálaváltozók
vektorának kinyerését és a pontszámok kiszámolását. 

### A txt átalakítása

A további műveletekhez az lenne az ideális, hogyha lenne egy listánk (`list`), amelynek elemei az egyes skálákhoz tartozó változók nevét tartalmazó vektorok lennének, a lista elemeinek neve pedig megegyezne a skálák neveivel. Vegyük észre, hogy a kapott txt fájl tartalma nem áll túlzottan távol egy ilyen lista megadásának módjától.

```r
# részlet
MOGQ_Social=(MOGQ1+MOGQ8+MOGQ15+MOGQ22)/4.
MOGQ_Escape=(MOGQ2+MOGQ9+MOGQ16+MOGQ23)/4.
...
```

Az elvárt alak ez lenne:

```r
skala_definiciok <- list(
    MOGQ_Social = c("MOGQ1", "MOGQ8", "MOGQ15", "MOGQ22"),
    MOGQ_Escape = c("MOGQ2", "MOGQ9", "MOGQ16", "MOGQ23"),
    ... 
)
```

Noha a kívánt átalakítást megfelelő R-parancsokkal is végrehajthatnánk, a következőkben egy pragmatikus megközelítést mutatunk be. Használjuk az RStudio-t arra, hogy kicseréljük a megfelelő karaktereket! Ehhez mindössze annyit kell tennünk, hogy megnyitjuk az RStudio-val az adott txt fájlt (`File > Open File...`), majd használjuk a CTRL+F billentyűkombinációt (vagy `Edit > Find...`). A keresési mezőbe írjuk be a cserélendő karaktert (pl. +), a Replace mezőbe pedig 
a kívánt karaktert (pl. ", "). Ezután kattintsunk a Replace melletti 'All' gombra.
A következő cseréket kell elvégeznünk:

Find  | Replace | Regex
------|---------|-------
+     | ", "    |  nem
=     | = c("   |  nem
)     | "),     |  nem
/.*   |         |  igen

Az utolsó cserénél reguláris kifejezést használunk (azaz be kell jelölni a Regex jelölőnégyzetet), amelyben a `/.*` azt jelzi, hogy `/` jel után bármilyen karakterek következhetnek. (Ezzel a lépéssel kitöröljük a sorok végéről a számokat és a pontot.)

A kapott szöveget egyszerűen bemásolhatjuk a skáladefiníciós listánkba:

```r
skala_definiciok <- list(
    MOGQ_Social = c("MOGQ1", "MOGQ8", "MOGQ15", "MOGQ22"),
    MOGQ_Escape = c("MOGQ2", "MOGQ9", "MOGQ16", "MOGQ23"),
    MOGQ_Competition = c("MOGQ3", "MOGQ10", "MOGQ17", "MOGQ24"),
    MOGQ_Coping = c("MOGQ4", "MOGQ11", "MOGQ18", "MOGQ25"),
    MOGQ_SkillDev = c("MOGQ5", "MOGQ12", "MOGQ19", "MOGQ26"),
    MOGQ_Fantasy = c("MOGQ6", "MOGQ13", "MOGQ20", "MOGQ27"),
    MOGQ_Recreation = c("MOGQ7", "MOGQ14", "MOGQ21"),
    POGQ_Preoccupation = c("POGQ1", "POGQ7"),
    POGQ_Immersion = c("POGQ2", "POGQ8", "POGQ13", "POGQ17"),
    POGQ_Withdrawal = c("POGQ3", "POGQ9", "POGQ14", "POGQ18"),
    POGQ_Overuse = c("POGQ4", "POGQ10", "POGQ15"),
    POGQ_IntConflicts = c("POGQ5", "POGQ11"),
    POGQ_SocIsolation = c("POGQ6", "POGQ12", "POGQ16"),
    BSI_Somatization = c("BSI2", "BSI7", "BSI23", "BSI29", "BSI30", "BSI33", "BSI37"),
    BSI_ObsComp = c("BSI5", "BSI15", "BSI26", "BSI27", "BSI32", "BSI36"),
    BSI_IntpersSens = c("BSI20", "BSI21", "BSI22", "BSI42"),
    BSI_Depression = c("BSI9", "BSI16", "BSI17", "BSI18", "BSI35", "BSI50"),
    BSI_Anxiety = c("BSI1", "BSI12", "BSI19", "BSI38", "BSI45", "BSI49"),
    BSI_Hostility = c("BSI6", "BSI13", "BSI40", "BSI41", "BSI46"),
    BSI_PhobicAnxiety = c("BSI8", "BSI28", "BSI31", "BSI43", "BSI47"),
    BSI_ParanoidId = c("BSI4", "BSI10", "BSI24", "BSI48", "BSI51"),
    BSI_Psychotiscism = c("BSI3", "BSI14", "BSI34", "BSI44", "BSI53"),
    GSI = c("BSI1", "BSI2", "BSI3", "BSI4", "BSI5", "BSI6", "BSI7", "BSI8", "BSI9", "BSI10", "BSI11", "BSI12", "BSI13", "BSI14", "BSI15", "BSI16", "BSI17", "BSI18", "BSI19", "BSI20", "BSI21", "BSI22", "BSI23", "BSI24", "BSI25", "BSI26", "BSI27", "BSI28", "BSI29", "BSI30", "BSI31", "BSI32", "BSI33", "BSI34", "BSI35", "BSI36", "BSI37", "BSI38", "BSI39", "BSI40", "BSI41", "BSI42", "BSI43", "BSI44", "BSI45", "BSI46", "BSI47", "BSI48", "BSI49", "BSI50", "BSI51", "BSI52", "BSI53")
)
```

### Skálapontok kiszámítása

Térjünk vissza a korábbi, "kézi" példához:

```r
MOGQ_social_itemek <- c("MOGQ1", "MOGQ8", "MOGQ15", "MOGQ22")
MOGQ_social <- rowMeans(dat[, MOGQ_social_itemek], na.rm = TRUE)
```

Vegyük észre, hogy a fenti sorokat a skáladefiníciós listánk segítségével immáron így is írhatnánk:

```r
itemek <- skala_definiciok[["MOGQ_social"]]
skala <- rowMeans(dat[, itemek], na.rm = TRUE)
```

Innentől akármelyik skálának a kiszámításához elég lenne az "MOGQ_social"-t átírni, amit akár megtehetnénk egy `for` ciklussal is:

```r
skala_nevek <- names(skala_definiciok)
for (n in skala_nevek) {
    itemek <- skala_definiciok[[n]]
    skala <- rowMeans(dat[, itemek], 
                      na.rm = TRUE)
}
```

Igen ám, de a fentebbi ciklus végeredményét mindig a `skala` változóhoz rendeljük hozzá, azaz ciklusunk folyton felülírja az előzőleg kiszámolt skálapontszámot.
Ezt kikerülhetnénk azzal, ha először létrehoznánk egy mátrixot (vagy data.frame-et), és a ciklusban csak a megfelelő oszlopot írnánk felül. Van azonban egy parancs (pontosabban parancsok egész családja, lásd `?lapply`), amely automatikusan összefűzi egy listába a ciklusban létrehozott változókat, azaz nem kell bajlódnunk az eredmény-változó előzetes megadásával. 


```r
skalapontok <- lapply(skala_nevek, 
                      function(n) {
                          itemek <- skala_definiciok[[n]]
                          rowMeans(dat[, itemek],
                                   na.rm = TRUE)
                          }
                      )
```

A `lapply` függvény első argumentuma egy vektor, második argumentuma pedig
egy függvény vagy egy függvény neve. (A `lapply` esetleges további argumentumai
az előzőleg megadott függvény egyéb lehetséges argumentumai.) A fentebbi sorokkal
tehát a következőre utasítjuk az R-et: 1) vedd a skala_nevek vektort, majd 2) minden egyes elemét helyettesítsd be abba az általunk definiált függvénybe, amely kiszámolja a `dat` adattáblánk megfelelő változóinak sorátlagait, és végül 3) a függvény által kiszámolt pontszám-vektorokat fűzd össze egy listába. 

A fentebbi sorok még mindig redundánsak kicsit; miért indexelünk a `skala_nevek` vektorral, azaz miért nem használjuk közvetlenül a `skala_definíciók` lista elemeit? Valóban, [emlékezzünk vissza](../sec3_basics/objects.html), hogy a lista valójában egy vektor. Azaz a fentebbi sorokat így is egyszerűsíthetnénk:

```r
skalapontok <- lapply(skala_definiciok, 
                      function(itemek) {
                          rowMeans(dat[, itemek],
                                   na.rm = TRUE)
                          }
                      )
```

A skálapontszámok számításának ez utóbbi módja azért is előnyösebb, mert így a `skalapontok` egy nevekkel ellátott lista lesz, azaz nem kell a `lapply` parancs után ezt is lefuttatnunk: `names(skalapontok) <- skala_nevek`. (Ez annak köszönhető, hogy ha a `lapply` argumentumában megadott, tág értelemben vett vektornak vannak nevei, akkor azok megőrződnek az eredmény-listában is.)

A skálapontszámokat kiszámoltuk, de van egy bökkenő: az elemzéseinkhez data.frame-re lenne szükség, azonban a `skalapontok` objektum egy lista. Semmi gond, alakítsuk át data.frame-mé:

```r
skalapontok <- as.data.frame(skalapontok)
```

### Leíró statiszikák, vizualizáció

Legkésőbb ezen a ponton érdemes leíró statisztikákat is lekérni:

```r
# töltsük be a psych csomagot
library(psych)

# kérjünk leíró statisztikákat csoportonkénti bontásban
describeBy(skalapontok, 
           group = dat[, c("Heavy_use", "Problematic")])
```

```
## Heavy_use: less than or equal to 4 h/day
## Problematic: non-disordered
##                    vars    n mean   sd median trimmed  mad  min  max range
## MOGQ_Social           1 1966 3.01 0.72   3.00    3.01 0.74 1.00 5.00  4.00
## MOGQ_Escape           2 1966 3.02 0.70   3.00    3.03 0.74 1.00 5.00  4.00
## MOGQ_Competition      3 1966 2.98 0.71   3.00    2.98 0.74 1.00 5.00  4.00
## MOGQ_Coping           4 1966 2.99 0.69   3.00    2.98 0.74 1.00 5.00  4.00
## MOGQ_SkillDev         5 1966 2.99 0.69   3.00    2.99 0.74 1.00 5.00  4.00
## MOGQ_Fantasy          6 1966 3.00 0.70   3.00    3.00 0.74 1.25 5.00  3.75
## MOGQ_Recreation       7 1966 3.00 0.81   3.00    3.01 0.99 1.00 5.00  4.00
## POGQ_Preoccupation    8 1966 2.70 0.90   2.50    2.68 0.74 1.00 5.00  4.00
## POGQ_Immersion        9 1966 3.02 0.71   3.00    3.02 0.74 1.25 5.00  3.75
## POGQ_Withdrawal      10 1966 2.36 0.68   2.25    2.33 0.74 1.00 5.00  4.00
## POGQ_Overuse         11 1966 3.03 0.82   3.00    3.03 0.99 1.00 5.00  4.00
## POGQ_IntConflicts    12 1966 2.97 1.01   3.00    2.96 0.74 1.00 5.00  4.00
## POGQ_SocIsolation    13 1966 3.02 0.82   3.00    3.03 0.99 1.00 5.00  4.00
## BSI_Somatization     14 1966 3.00 0.53   3.00    3.01 0.64 1.14 4.71  3.57
## BSI_ObsComp          15 1966 2.80 0.56   2.83    2.80 0.49 1.17 4.67  3.50
## BSI_IntpersSens      16 1966 2.70 0.68   2.75    2.70 0.74 1.00 5.00  4.00
## BSI_Depression       17 1966 2.28 0.74   2.17    2.21 0.74 1.00 5.00  4.00
## BSI_Anxiety          18 1966 2.78 0.54   2.83    2.78 0.49 1.33 4.83  3.50
## BSI_Hostility        19 1966 2.26 0.65   2.20    2.21 0.59 1.00 5.00  4.00
## BSI_PhobicAnxiety    20 1966 2.33 0.59   2.20    2.30 0.59 1.00 5.00  4.00
## BSI_ParanoidId       21 1966 2.53 0.66   2.40    2.51 0.59 1.00 5.00  4.00
## BSI_Psychotiscism    22 1966 2.69 0.59   2.60    2.68 0.59 1.00 4.60  3.60
## GSI                  23 1966 2.61 0.27   2.58    2.60 0.25 1.91 3.98  2.08
##                     skew kurtosis   se
## MOGQ_Social         0.03    -0.41 0.02
## MOGQ_Escape        -0.02    -0.43 0.02
## MOGQ_Competition    0.02    -0.38 0.02
## MOGQ_Coping         0.02    -0.31 0.02
## MOGQ_SkillDev       0.02    -0.27 0.02
## MOGQ_Fantasy       -0.04    -0.37 0.02
## MOGQ_Recreation    -0.03    -0.48 0.02
## POGQ_Preoccupation  0.14    -0.52 0.02
## POGQ_Immersion      0.04    -0.37 0.02
## POGQ_Withdrawal     0.47     0.35 0.02
## POGQ_Overuse        0.03    -0.53 0.02
## POGQ_IntConflicts   0.02    -0.66 0.02
## POGQ_SocIsolation  -0.08    -0.46 0.02
## BSI_Somatization   -0.05    -0.14 0.01
## BSI_ObsComp         0.06    -0.16 0.01
## BSI_IntpersSens     0.12    -0.21 0.02
## BSI_Depression      0.81     0.36 0.02
## BSI_Anxiety         0.04    -0.19 0.01
## BSI_Hostility       0.82     1.06 0.01
## BSI_PhobicAnxiety   0.58     0.61 0.01
## BSI_ParanoidId      0.38     0.04 0.01
## BSI_Psychotiscism   0.06    -0.20 0.01
## GSI                 0.68     0.64 0.01
## -------------------------------------------------------- 
## Heavy_use: more than 4 h/day
## Problematic: non-disordered
##                    vars   n mean   sd median trimmed  mad  min  max range
## MOGQ_Social           1 667 3.01 0.71   3.00    3.01 0.74 1.25 4.75  3.50
## MOGQ_Escape           2 667 3.02 0.68   3.00    3.04 0.74 1.00 4.75  3.75
## MOGQ_Competition      3 667 3.01 0.69   3.00    3.00 0.74 1.25 5.00  3.75
## MOGQ_Coping           4 667 3.00 0.68   3.00    3.00 0.74 1.00 4.75  3.75
## MOGQ_SkillDev         5 667 3.04 0.70   3.00    3.05 0.74 1.00 4.75  3.75
## MOGQ_Fantasy          6 667 2.99 0.69   3.00    2.99 0.74 1.00 5.00  4.00
## MOGQ_Recreation       7 667 2.97 0.82   3.00    2.96 0.99 1.00 5.00  4.00
## POGQ_Preoccupation    8 667 2.96 0.91   3.00    2.98 0.74 1.00 5.00  4.00
## POGQ_Immersion        9 667 2.99 0.70   3.00    2.97 0.74 1.25 5.00  3.75
## POGQ_Withdrawal      10 667 2.58 0.72   2.50    2.55 0.74 1.00 4.75  3.75
## POGQ_Overuse         11 667 3.09 0.82   3.00    3.08 0.99 1.00 5.00  4.00
## POGQ_IntConflicts    12 667 2.96 0.93   3.00    2.97 0.74 1.00 5.00  4.00
## POGQ_SocIsolation    13 667 3.04 0.82   3.00    3.04 0.99 1.00 5.00  4.00
## BSI_Somatization     14 667 3.00 0.54   3.00    3.00 0.64 1.43 4.57  3.14
## BSI_ObsComp          15 667 2.82 0.55   2.83    2.82 0.49 1.33 4.80  3.47
## BSI_IntpersSens      16 667 2.73 0.68   2.75    2.73 0.74 1.00 5.00  4.00
## BSI_Depression       17 667 2.36 0.78   2.17    2.30 0.74 1.00 5.00  4.00
## BSI_Anxiety          18 667 2.77 0.57   2.83    2.77 0.49 1.17 4.40  3.23
## BSI_Hostility        19 667 2.33 0.70   2.20    2.28 0.59 1.00 5.00  4.00
## BSI_PhobicAnxiety    20 667 2.34 0.60   2.20    2.31 0.59 1.00 5.00  4.00
## BSI_ParanoidId       21 667 2.60 0.64   2.60    2.58 0.59 1.00 4.60  3.60
## BSI_Psychotiscism    22 667 2.71 0.62   2.60    2.71 0.59 1.20 4.50  3.30
## GSI                  23 667 2.65 0.29   2.62    2.63 0.28 1.94 3.75  1.81
##                     skew kurtosis   se
## MOGQ_Social         0.05    -0.46 0.03
## MOGQ_Escape        -0.23    -0.31 0.03
## MOGQ_Competition    0.05    -0.28 0.03
## MOGQ_Coping        -0.04    -0.16 0.03
## MOGQ_SkillDev      -0.09    -0.33 0.03
## MOGQ_Fantasy        0.06    -0.20 0.03
## MOGQ_Recreation     0.07    -0.34 0.03
## POGQ_Preoccupation -0.16    -0.67 0.04
## POGQ_Immersion      0.14    -0.39 0.03
## POGQ_Withdrawal     0.41    -0.06 0.03
## POGQ_Overuse        0.07    -0.37 0.03
## POGQ_IntConflicts  -0.04    -0.43 0.04
## POGQ_SocIsolation  -0.01    -0.54 0.03
## BSI_Somatization   -0.08    -0.13 0.02
## BSI_ObsComp        -0.01    -0.18 0.02
## BSI_IntpersSens     0.03    -0.12 0.03
## BSI_Depression      0.69     0.14 0.03
## BSI_Anxiety         0.04    -0.40 0.02
## BSI_Hostility       0.75     0.82 0.03
## BSI_PhobicAnxiety   0.59     0.79 0.02
## BSI_ParanoidId      0.30    -0.12 0.02
## BSI_Psychotiscism   0.07    -0.45 0.02
## GSI                 0.61     0.44 0.01
## -------------------------------------------------------- 
## Heavy_use: less than or equal to 4 h/day
## Problematic: disordered
##                    vars    n mean   sd median trimmed  mad  min  max range
## MOGQ_Social           1 1936 3.02 0.70   3.00    3.02 0.74 1.00 5.00  4.00
## MOGQ_Escape           2 1936 3.00 0.70   3.00    3.00 0.74 1.00 5.00  4.00
## MOGQ_Competition      3 1936 2.99 0.70   3.00    2.99 0.74 1.00 5.00  4.00
## MOGQ_Coping           4 1936 3.01 0.69   3.00    3.01 0.74 1.00 5.00  4.00
## MOGQ_SkillDev         5 1936 2.99 0.70   3.00    2.99 0.74 1.00 5.00  4.00
## MOGQ_Fantasy          6 1936 3.01 0.69   3.00    3.01 0.74 1.00 5.00  4.00
## MOGQ_Recreation       7 1936 2.99 0.84   3.00    2.99 0.99 1.00 5.00  4.00
## POGQ_Preoccupation    8 1936 2.71 0.88   2.50    2.69 0.74 1.00 5.00  4.00
## POGQ_Immersion        9 1936 3.02 0.71   3.00    3.02 0.74 1.00 5.00  4.00
## POGQ_Withdrawal      10 1936 2.38 0.67   2.25    2.36 0.74 1.00 5.00  4.00
## POGQ_Overuse         11 1936 3.01 0.85   3.00    3.02 0.99 1.00 5.00  4.00
## POGQ_IntConflicts    12 1936 3.01 1.00   3.00    3.01 0.74 1.00 5.00  4.00
## POGQ_SocIsolation    13 1936 3.00 0.80   3.00    3.01 0.99 1.00 5.00  4.00
## BSI_Somatization     14 1936 3.01 0.54   3.00    3.01 0.64 1.29 4.86  3.57
## BSI_ObsComp          15 1936 2.79 0.56   2.83    2.79 0.49 1.00 4.80  3.80
## BSI_IntpersSens      16 1936 2.68 0.68   2.75    2.67 0.74 1.00 5.00  4.00
## BSI_Depression       17 1936 2.30 0.73   2.17    2.23 0.74 1.00 5.00  4.00
## BSI_Anxiety          18 1936 2.80 0.57   2.83    2.80 0.49 1.17 4.83  3.67
## BSI_Hostility        19 1936 2.24 0.62   2.20    2.20 0.59 1.00 4.60  3.60
## BSI_PhobicAnxiety    20 1936 2.33 0.58   2.40    2.31 0.59 1.00 5.00  4.00
## BSI_ParanoidId       21 1936 2.55 0.62   2.60    2.53 0.59 1.00 5.00  4.00
## BSI_Psychotiscism    22 1936 2.66 0.60   2.60    2.65 0.59 1.00 4.75  3.75
## GSI                  23 1936 2.62 0.26   2.58    2.60 0.25 1.98 3.62  1.64
##                     skew kurtosis   se
## MOGQ_Social         0.05    -0.36 0.02
## MOGQ_Escape         0.00    -0.36 0.02
## MOGQ_Competition    0.01    -0.30 0.02
## MOGQ_Coping         0.01    -0.31 0.02
## MOGQ_SkillDev       0.00    -0.42 0.02
## MOGQ_Fantasy       -0.06    -0.28 0.02
## MOGQ_Recreation     0.02    -0.47 0.02
## POGQ_Preoccupation  0.16    -0.49 0.02
## POGQ_Immersion     -0.02    -0.40 0.02
## POGQ_Withdrawal     0.44     0.24 0.02
## POGQ_Overuse       -0.04    -0.56 0.02
## POGQ_IntConflicts  -0.06    -0.65 0.02
## POGQ_SocIsolation  -0.02    -0.32 0.02
## BSI_Somatization    0.01     0.02 0.01
## BSI_ObsComp         0.08    -0.11 0.01
## BSI_IntpersSens     0.12    -0.23 0.02
## BSI_Depression      0.85     0.66 0.02
## BSI_Anxiety         0.15    -0.07 0.01
## BSI_Hostility       0.67     0.60 0.01
## BSI_PhobicAnxiety   0.43     0.50 0.01
## BSI_ParanoidId      0.37     0.40 0.01
## BSI_Psychotiscism   0.10    -0.18 0.01
## GSI                 0.66     0.58 0.01
## -------------------------------------------------------- 
## Heavy_use: more than 4 h/day
## Problematic: disordered
##                    vars   n mean   sd median trimmed  mad  min  max range
## MOGQ_Social           1 707 3.03 0.71   3.00    3.03 0.74 1.25 5.00  3.75
## MOGQ_Escape           2 707 3.00 0.71   3.00    3.01 0.74 1.00 5.00  4.00
## MOGQ_Competition      3 707 2.99 0.69   3.00    2.99 0.74 1.25 4.75  3.50
## MOGQ_Coping           4 707 3.02 0.70   3.00    3.03 0.74 1.00 4.75  3.75
## MOGQ_SkillDev         5 707 3.01 0.70   3.00    3.01 0.74 1.00 5.00  4.00
## MOGQ_Fantasy          6 707 2.94 0.69   3.00    2.93 0.74 1.00 4.75  3.75
## MOGQ_Recreation       7 707 2.97 0.86   3.00    2.97 0.99 1.00 5.00  4.00
## POGQ_Preoccupation    8 707 2.92 0.92   3.00    2.92 0.74 1.00 5.00  4.00
## POGQ_Immersion        9 707 3.03 0.70   3.00    3.04 0.74 1.00 5.00  4.00
## POGQ_Withdrawal      10 707 2.49 0.72   2.50    2.47 0.74 1.00 4.75  3.75
## POGQ_Overuse         11 707 3.03 0.81   3.00    3.03 0.99 1.00 5.00  4.00
## POGQ_IntConflicts    12 707 3.01 0.99   3.00    3.01 0.74 1.00 5.00  4.00
## POGQ_SocIsolation    13 707 3.02 0.81   3.00    3.01 0.99 1.00 5.00  4.00
## BSI_Somatization     14 707 3.01 0.54   3.00    3.01 0.64 1.29 4.57  3.29
## BSI_ObsComp          15 707 2.86 0.58   2.83    2.86 0.49 1.33 5.00  3.67
## BSI_IntpersSens      16 707 2.73 0.66   2.75    2.72 0.74 1.00 4.75  3.75
## BSI_Depression       17 707 2.43 0.82   2.33    2.36 0.74 1.00 5.00  4.00
## BSI_Anxiety          18 707 2.79 0.55   2.83    2.78 0.49 1.33 4.67  3.33
## BSI_Hostility        19 707 2.33 0.70   2.20    2.28 0.59 1.00 4.50  3.50
## BSI_PhobicAnxiety    20 707 2.38 0.60   2.40    2.35 0.59 1.00 5.00  4.00
## BSI_ParanoidId       21 707 2.64 0.68   2.60    2.62 0.59 1.00 4.67  3.67
## BSI_Psychotiscism    22 707 2.70 0.59   2.60    2.69 0.59 1.00 4.75  3.75
## GSI                  23 707 2.67 0.29   2.64    2.65 0.28 1.98 3.59  1.61
##                     skew kurtosis   se
## MOGQ_Social        -0.07    -0.38 0.03
## MOGQ_Escape        -0.05    -0.24 0.03
## MOGQ_Competition    0.12    -0.27 0.03
## MOGQ_Coping        -0.09    -0.45 0.03
## MOGQ_SkillDev       0.01     0.01 0.03
## MOGQ_Fantasy        0.04    -0.35 0.03
## MOGQ_Recreation     0.02    -0.48 0.03
## POGQ_Preoccupation  0.03    -0.67 0.03
## POGQ_Immersion     -0.01    -0.39 0.03
## POGQ_Withdrawal     0.33    -0.18 0.03
## POGQ_Overuse        0.07    -0.43 0.03
## POGQ_IntConflicts   0.02    -0.68 0.04
## POGQ_SocIsolation   0.08    -0.46 0.03
## BSI_Somatization   -0.08    -0.28 0.02
## BSI_ObsComp         0.07     0.04 0.02
## BSI_IntpersSens     0.18    -0.27 0.02
## BSI_Depression      0.66    -0.09 0.03
## BSI_Anxiety         0.09    -0.25 0.02
## BSI_Hostility       0.66     0.33 0.03
## BSI_PhobicAnxiety   0.51     0.51 0.02
## BSI_ParanoidId      0.18    -0.18 0.03
## BSI_Psychotiscism   0.10     0.06 0.02
## GSI                 0.51     0.03 0.01
```

A változóink eloszlását még könnyebben ellenőrizhetnénk ábrák készítésével. Ezt ezúttal - később kifejtett indok miatt - az elemzési részben tesszük meg.

## Végső adattábla elkészítése

Néhány lépés még mindig hiányzik. Az elemzéseinkhez szükség lesz a 'Heavy_use' és a 'Problematic' változókra is, illetve előnyös lehet megtartani a személyi azonosítókat is ('Sorszám' változó), ezeket viszont a `skalapontok` objektum nem tartalmazza. Nem kell kétségbe esni, a rendelkezésre álló adatstruktúrákból a végső adattábla a [tanult](../sec3_basics/combine_objects.md) művelettel létrehozható:

```r
final_dat <- data.frame(skalapontok, 
                        dat[, c("Sorszam", "Heavy_use", "Problematic")])
```

Döntést kell hoznunk arról is, hogy mi legyen a hiányzó értékekkel rendelkező személyeinkkel. Az egyik megoldás az lenne, ha valamilyen módszerrel imputálnánk ("pótolnánk") a hiányzó adatokat. A másik megoldás az, hogy a hiányzó értékkel rendelkező sorokat egyszerűen kihagyjuk az elemzésből. Most az utóbbi megoldást választjuk:

```r
final_dat <- na.omit(final_dat)
```

(Az `na.omit()` függvény nemcsak kihagyja a hiányzó értékkel rendelkező sorokat, hanem egy külön attribútumban [lásd `attr(final_dat, "na.action")`] eltárolja a kihagyott sorok sorszámát is.)

Ne feledjük, az elemzéseket a standardizált skálapontszámokon kell majd végeznünk. A standardizálás nagyon egyszerűen elvégezhető a `scale()` függvénnyel:

```r
# standardizálandó változók:
skala_nevek <- colnames(skalapontok)
final_dat[, skala_nevek] <- scale(final_dat[, skala_nevek])
```

Innentől tényleg nem marad más hátra, mint elmenteni a végső adattáblánkat, majd hozzákezdeni az adatok elemzéséhez. 

```r
# adattable mentese
saveRDS(final_dat, 
        file = file.path("data", "prepared_data.rds"))
```

## A teljes szkript

A könnyebb futtathatóság végett közöljük a végleges előkészítő szkriptet (csak a tényleges átalakításokat végző lépésekkel):

```r
# beolvasás
library(foreign)
dat <- read.spss(file.path("data", "gaming_random.sav"),
                 to.data.frame = TRUE)

# integer-ré alakítás
likert_valtozok <- grep("MOGQ|POGQ|BSI", 
                        colnames(dat), 
                        value = TRUE)
for (i in likert_valtozok) {
    dat[, i] <- as.integer(dat[, i])
}

# skáladefiníciók
skala_definiciok <- list(
    MOGQ_Social = c("MOGQ1", "MOGQ8", "MOGQ15", "MOGQ22"),
    MOGQ_Escape = c("MOGQ2", "MOGQ9", "MOGQ16", "MOGQ23"),
    MOGQ_Competition = c("MOGQ3", "MOGQ10", "MOGQ17", "MOGQ24"),
    MOGQ_Coping = c("MOGQ4", "MOGQ11", "MOGQ18", "MOGQ25"),
    MOGQ_SkillDev = c("MOGQ5", "MOGQ12", "MOGQ19", "MOGQ26"),
    MOGQ_Fantasy = c("MOGQ6", "MOGQ13", "MOGQ20", "MOGQ27"),
    MOGQ_Recreation = c("MOGQ7", "MOGQ14", "MOGQ21"),
    POGQ_Preoccupation = c("POGQ1", "POGQ7"),
    POGQ_Immersion = c("POGQ2", "POGQ8", "POGQ13", "POGQ17"),
    POGQ_Withdrawal = c("POGQ3", "POGQ9", "POGQ14", "POGQ18"),
    POGQ_Overuse = c("POGQ4", "POGQ10", "POGQ15"),
    POGQ_IntConflicts = c("POGQ5", "POGQ11"),
    POGQ_SocIsolation = c("POGQ6", "POGQ12", "POGQ16"),
    BSI_Somatization = c("BSI2", "BSI7", "BSI23", "BSI29", "BSI30", "BSI33", "BSI37"),
    BSI_ObsComp = c("BSI5", "BSI15", "BSI26", "BSI27", "BSI32", "BSI36"),
    BSI_IntpersSens = c("BSI20", "BSI21", "BSI22", "BSI42"),
    BSI_Depression = c("BSI9", "BSI16", "BSI17", "BSI18", "BSI35", "BSI50"),
    BSI_Anxiety = c("BSI1", "BSI12", "BSI19", "BSI38", "BSI45", "BSI49"),
    BSI_Hostility = c("BSI6", "BSI13", "BSI40", "BSI41", "BSI46"),
    BSI_PhobicAnxiety = c("BSI8", "BSI28", "BSI31", "BSI43", "BSI47"),
    BSI_ParanoidId = c("BSI4", "BSI10", "BSI24", "BSI48", "BSI51"),
    BSI_Psychotiscism = c("BSI3", "BSI14", "BSI34", "BSI44", "BSI53"),
    GSI = c("BSI1", "BSI2", "BSI3", "BSI4", "BSI5", "BSI6", "BSI7", "BSI8", "BSI9", "BSI10", "BSI11", "BSI12", "BSI13", "BSI14", "BSI15", "BSI16", "BSI17", "BSI18", "BSI19", "BSI20", "BSI21", "BSI22", "BSI23", "BSI24", "BSI25", "BSI26", "BSI27", "BSI28", "BSI29", "BSI30", "BSI31", "BSI32", "BSI33", "BSI34", "BSI35", "BSI36", "BSI37", "BSI38", "BSI39", "BSI40", "BSI41", "BSI42", "BSI43", "BSI44", "BSI45", "BSI46", "BSI47", "BSI48", "BSI49", "BSI50", "BSI51", "BSI52", "BSI53")
)

# skálapontszámok számítása
skalapontok <- lapply(skala_definiciok, 
                      function(itemek) {
                          rowMeans(dat[, itemek],
                                   na.rm = TRUE)
                          }
                      )
skalapontok <- as.data.frame(skalapontok)

# végső adattábla
final_dat <- data.frame(skalapontok, 
                        dat[, c("Sorszam", "Heavy_use", "Problematic")])
final_dat <- na.omit(final_dat)
skala_nevek <- colnames(skalapontok)
final_dat[, skala_nevek] <- scale(final_dat[, skala_nevek])

# mentés
saveRDS(final_dat, 
        file = file.path("data", "prepared_data.rds"))
```


