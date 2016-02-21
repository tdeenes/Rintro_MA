# Adatexploráció, ábrázolás 




## A kísérleti dizájn vizsgálata, leíró statisztikák
- elvileg keresztezett random hatásaink vannak: minden személynek minden szót bemutattak, pontosan egyszer

```r
freq <- with(lexdec, table(Subject, Word))
# a freq mátrix túl nagy, a példához elég egy kis részlete
freq[1:5, 1:5]
```

```
##        Word
## Subject almond ant apple apricot asparagus
##      A1      1   1     1       1         1
##      A2      1   1     1       1         1
##      A3      1   1     1       1         1
##      C       1   1     1       1         1
##      D       1   1     1       1         1
```

```r
# tökéletesen keresztezett, ismétlés nélküli dizájn
table(freq)
```

```
## freq
##    1 
## 1659
```

- létrehoztunk egy beágyazott hatást is: a szavak a szótár egy-egy oldaláról származnak

```r
with(lexdec, table(Word, Page))
```

```
##             Page
## Word         page1 page2 page3 page4 page5 page6 page7 page8 page9 page10
##   almond        21     0     0     0     0     0     0     0     0      0
##   ant           21     0     0     0     0     0     0     0     0      0
##   apple         21     0     0     0     0     0     0     0     0      0
##   apricot       21     0     0     0     0     0     0     0     0      0
##   asparagus     21     0     0     0     0     0     0     0     0      0
##   avocado       21     0     0     0     0     0     0     0     0      0
##   banana        21     0     0     0     0     0     0     0     0      0
##   bat           21     0     0     0     0     0     0     0     0      0
##   beaver         0    21     0     0     0     0     0     0     0      0
##   bee            0    21     0     0     0     0     0     0     0      0
##   beetroot       0    21     0     0     0     0     0     0     0      0
##   blackberry     0    21     0     0     0     0     0     0     0      0
##   blueberry      0    21     0     0     0     0     0     0     0      0
##   broccoli       0    21     0     0     0     0     0     0     0      0
##   bunny          0    21     0     0     0     0     0     0     0      0
##   butterfly      0    21     0     0     0     0     0     0     0      0
##   camel          0     0    21     0     0     0     0     0     0      0
##   carrot         0     0    21     0     0     0     0     0     0      0
##   cat            0     0    21     0     0     0     0     0     0      0
##   cherry         0     0    21     0     0     0     0     0     0      0
##   chicken        0     0    21     0     0     0     0     0     0      0
##   clove          0     0    21     0     0     0     0     0     0      0
##   crocodile      0     0    21     0     0     0     0     0     0      0
##   cucumber       0     0    21     0     0     0     0     0     0      0
##   dog            0     0     0    21     0     0     0     0     0      0
##   dolphin        0     0     0    21     0     0     0     0     0      0
##   donkey         0     0     0    21     0     0     0     0     0      0
##   eagle          0     0     0    21     0     0     0     0     0      0
##   eggplant       0     0     0    21     0     0     0     0     0      0
##   elephant       0     0     0    21     0     0     0     0     0      0
##   fox            0     0     0    21     0     0     0     0     0      0
##   frog           0     0     0    21     0     0     0     0     0      0
##   gherkin        0     0     0     0    21     0     0     0     0      0
##   goat           0     0     0     0    21     0     0     0     0      0
##   goose          0     0     0     0    21     0     0     0     0      0
##   grape          0     0     0     0    21     0     0     0     0      0
##   gull           0     0     0     0    21     0     0     0     0      0
##   hedgehog       0     0     0     0    21     0     0     0     0      0
##   horse          0     0     0     0    21     0     0     0     0      0
##   kiwi           0     0     0     0    21     0     0     0     0      0
##   leek           0     0     0     0     0    21     0     0     0      0
##   lemon          0     0     0     0     0    21     0     0     0      0
##   lettuce        0     0     0     0     0    21     0     0     0      0
##   lion           0     0     0     0     0    21     0     0     0      0
##   magpie         0     0     0     0     0    21     0     0     0      0
##   melon          0     0     0     0     0    21     0     0     0      0
##   mole           0     0     0     0     0    21     0     0     0      0
##   monkey         0     0     0     0     0    21     0     0     0      0
##   moose          0     0     0     0     0     0    21     0     0      0
##   mouse          0     0     0     0     0     0    21     0     0      0
##   mushroom       0     0     0     0     0     0    21     0     0      0
##   mustard        0     0     0     0     0     0    21     0     0      0
##   olive          0     0     0     0     0     0    21     0     0      0
##   orange         0     0     0     0     0     0    21     0     0      0
##   owl            0     0     0     0     0     0    21     0     0      0
##   paprika        0     0     0     0     0     0    21     0     0      0
##   peanut         0     0     0     0     0     0     0    21     0      0
##   pear           0     0     0     0     0     0     0    21     0      0
##   pig            0     0     0     0     0     0     0    21     0      0
##   pineapple      0     0     0     0     0     0     0    21     0      0
##   potato         0     0     0     0     0     0     0    21     0      0
##   radish         0     0     0     0     0     0     0    21     0      0
##   reindeer       0     0     0     0     0     0     0    21     0      0
##   shark          0     0     0     0     0     0     0    21     0      0
##   sheep          0     0     0     0     0     0     0     0    21      0
##   snake          0     0     0     0     0     0     0     0    21      0
##   spider         0     0     0     0     0     0     0     0    21      0
##   squid          0     0     0     0     0     0     0     0    21      0
##   squirrel       0     0     0     0     0     0     0     0    21      0
##   stork          0     0     0     0     0     0     0     0    21      0
##   strawberry     0     0     0     0     0     0     0     0    21      0
##   swan           0     0     0     0     0     0     0     0    21      0
##   tomato         0     0     0     0     0     0     0     0     0     21
##   tortoise       0     0     0     0     0     0     0     0     0     21
##   vulture        0     0     0     0     0     0     0     0     0     21
##   walnut         0     0     0     0     0     0     0     0     0     21
##   wasp           0     0     0     0     0     0     0     0     0     21
##   whale          0     0     0     0     0     0     0     0     0     21
##   woodpecker     0     0     0     0     0     0     0     0     0     21
```

Fontos, hogy sose kódoljunk úgy változókat, hogy ne legyen egyértelmű, hogy keresztezett vagy beágyazott hatásokról van-e szó. Magyarán ha hierarchikus változóink vannak (pl. személy << iskola, vagy jelen példában szó << szótári oldal),
akkor az alsóbb szinten is alkalmazzunk egyedi azonosítókat. Jelen példánál maradva,
ahol minden szótári oldalról 8-8 szó szerepel, hiba lenne a szavakat "word1",
"word2", "word3", ..., "word8"-ként kódolni, hiszen az egyik oldal "word1" 
szavának semmi köze nincsen a másik oldal "word1" szavához. 

```r
# tegyük fel, hogy a Word változót word1, word2, ... word8-ként kódoltuk
# a Page minden szintjén
lexdec$WordWrong <- paste0(
    "word", 
    as.integer(lexdec$Word) - 8*(as.integer(lexdec$Page)-1))

# innentől a keresztgyakorisági tábla nem mutatja meg, hogy
# a 'word' faktor a 'page' faktorunkba van ágyazva
with(lexdec, table(WordWrong, Page))
```

```
##          Page
## WordWrong page1 page2 page3 page4 page5 page6 page7 page8 page9 page10
##     word1    21    21    21    21    21    21    21    21    21     21
##     word2    21    21    21    21    21    21    21    21    21     21
##     word3    21    21    21    21    21    21    21    21    21     21
##     word4    21    21    21    21    21    21    21    21    21     21
##     word5    21    21    21    21    21    21    21    21    21     21
##     word6    21    21    21    21    21    21    21    21    21     21
##     word7    21    21    21    21    21    21    21    21    21     21
##     word8    21    21    21    21    21    21    21    21    21      0
```

- csak a helyes válaszokat akarjuk elemezni: szűrjük le az adatokat és
válasszuk ki a releváns változókat

```r
lexdec_corr <- subset(lexdec, Correct == "correct",
                      select = c(Subject, RT, Trial, NativeLanguage, 
                                 Word, Class, Page))
```

- kérjünk leíró statisztikákat a kérdéses változókra (a _psych_ csomagot fogom használni, de egyebet is lehetne)

```r
# általános leíró statisztikák
summary(lexdec_corr)
```

```
##     Subject           RT            Trial       NativeLanguage
##  A3     :  79   Min.   :5.566   Min.   : 23.0   English:920   
##  I      :  79   1st Qu.:6.148   1st Qu.: 64.0   Other  :674   
##  R2     :  79   Median :6.429   Median :106.0                 
##  W2     :  79   Mean   :6.438   Mean   :104.9                 
##  A1     :  78   3rd Qu.:6.686   3rd Qu.:146.0                 
##  C      :  78   Max.   :7.861   Max.   :185.0                 
##  (Other):1122                                                 
##       Word         Class          Page    
##  ant    :  21   animal:884   page2  :166  
##  apple  :  21   plant :710   page3  :165  
##  apricot:  21                page6  :164  
##  avocado:  21                page8  :163  
##  banana :  21                page1  :162  
##  beaver :  21                page4  :162  
##  (Other):1468                (Other):612
```

```r
# példa: válaszidők statisztikái szavanként, ferdeségi mutatóval
with(lexdec_corr, psych::describeBy(RT, Subject, skew = TRUE))
```

```
## group: A1
##   vars  n mean   sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 78 6.34 0.36   6.34    6.33 0.35 5.57 7.15  1.59 0.18    -0.61 0.04
## -------------------------------------------------------- 
## group: A2
##   vars  n mean   sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 76 6.28 0.33   6.28    6.26 0.31 5.61 7.09  1.48 0.42    -0.49 0.04
## -------------------------------------------------------- 
## group: A3
##   vars  n mean   sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 79 6.45 0.34   6.49    6.44 0.35 5.84 7.43  1.58 0.15     -0.5 0.04
## -------------------------------------------------------- 
## group: C
##   vars  n mean   sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 78 6.38 0.34   6.37    6.36 0.33 5.83 7.32  1.49  0.4     -0.3 0.04
## -------------------------------------------------------- 
## group: D
##   vars  n mean   sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 76 6.46 0.36   6.49    6.45 0.36 5.83 7.38  1.55  0.4    -0.28 0.04
## -------------------------------------------------------- 
## group: I
##   vars  n mean   sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 79 6.31 0.36   6.32     6.3 0.36 5.57 7.37  1.79 0.23    -0.18 0.04
## -------------------------------------------------------- 
## group: J
##   vars  n mean   sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 67 6.33 0.33   6.34    6.32 0.35 5.71 6.96  1.25 0.07     -0.9 0.04
## -------------------------------------------------------- 
## group: K
##   vars  n mean   sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 73 6.25 0.33    6.3    6.25 0.39 5.63 7.12   1.5 0.16    -0.58 0.04
## -------------------------------------------------------- 
## group: M1
##   vars  n mean  sd median trimmed mad  min  max range skew kurtosis   se
## 1    1 76 6.23 0.3   6.27    6.22 0.3 5.71 6.93  1.22 0.05    -0.72 0.03
## -------------------------------------------------------- 
## group: M2
##   vars  n mean  sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 75 6.57 0.4   6.58    6.56 0.33 5.88 7.54  1.66 0.28    -0.27 0.05
## -------------------------------------------------------- 
## group: P
##   vars  n mean   sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 78 6.48 0.35    6.5    6.47 0.37 5.87 7.17  1.29 0.02       -1 0.04
## -------------------------------------------------------- 
## group: R1
##   vars  n mean   sd median trimmed  mad  min max range skew kurtosis   se
## 1    1 74 6.36 0.36   6.37    6.34 0.37 5.73 7.5  1.77 0.58     0.24 0.04
## -------------------------------------------------------- 
## group: R2
##   vars  n mean   sd median trimmed  mad  min  max range  skew kurtosis
## 1    1 79 6.53 0.31   6.55    6.53 0.34 5.89 7.09  1.19 -0.18    -0.89
##     se
## 1 0.03
## -------------------------------------------------------- 
## group: R3
##   vars  n mean   sd median trimmed  mad  min  max range  skew kurtosis
## 1    1 77 6.44 0.32   6.46    6.44 0.36 5.82 7.13  1.31 -0.01    -0.83
##     se
## 1 0.04
## -------------------------------------------------------- 
## group: S
##   vars  n mean   sd median trimmed mad  min  max range skew kurtosis   se
## 1    1 78 6.43 0.36   6.45    6.43 0.4 5.69 7.17  1.48    0    -0.81 0.04
## -------------------------------------------------------- 
## group: T1
##   vars  n mean   sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 76 6.42 0.34   6.43    6.41 0.33 5.77 7.42  1.65 0.26    -0.27 0.04
## -------------------------------------------------------- 
## group: T2
##   vars  n mean  sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 72 6.85 0.4   6.92    6.85 0.33 6.04 7.86  1.82 0.02    -0.36 0.05
## -------------------------------------------------------- 
## group: V
##   vars  n mean   sd median trimmed  mad  min max range skew kurtosis   se
## 1    1 76 6.62 0.34   6.61    6.61 0.37 6.08 7.6  1.51 0.25    -0.57 0.04
## -------------------------------------------------------- 
## group: W1
##   vars  n mean  sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 76 6.31 0.3   6.31     6.3 0.35 5.82 7.15  1.33  0.4    -0.61 0.03
## -------------------------------------------------------- 
## group: W2
##   vars  n mean   sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 79 6.52 0.35   6.52    6.51 0.37 5.85 7.29  1.44 0.08    -0.72 0.04
## -------------------------------------------------------- 
## group: Z
##   vars  n mean   sd median trimmed  mad  min  max range skew kurtosis   se
## 1    1 72 6.65 0.39   6.68    6.64 0.37 5.92 7.41  1.49    0    -0.83 0.05
```

## Ábrázolás

A következőkben ggplot ábrákkal megvizsgáljuk, hogy milyen a hiányzó adatok
mintázata, illetve hogyan alakul a válaszidők eloszlása különböző csoportosító
szempontok alapján.

- hiányzó adatok (amiatt, hogy csak a helyes válaszokat elemezzük):

```r
library(ggplot2)
ggplot(lexdec_corr, aes(x = Subject, y = Word)) + 
    geom_tile()
```

![plot of chunk unnamed-chunk-7](figure/unnamed-chunk-7-1.png)

- válaszidők személyenként:

```r
# Subject
ggplot(lexdec_corr, aes(x = Subject, y = RT, col = NativeLanguage)) + 
    geom_boxplot() + 
    theme_bw()
```

![plot of chunk unnamed-chunk-8](figure/unnamed-chunk-8-1.png)

- válaszidők szavanként és oldalanként

```r
# Page & Word
ggplot(lexdec_corr, aes(x = Word, y = RT, col = Page)) + 
    geom_boxplot() + 
    theme_bw() + 
    theme(axis.text.x = element_text(angle = 90, hjust = 1))
```

![plot of chunk unnamed-chunk-9](figure/unnamed-chunk-9-1.png)

- válaszidők eloszlása az anyanyelv és az ingerosztály (állat/növény) függvényében

```r
# Class & NativeLanguage (boxplot)
ggplot(lexdec_corr, aes(x = NativeLanguage, y = RT, col = Class)) + 
    geom_boxplot() + 
    theme_bw()
```

![plot of chunk unnamed-chunk-10](figure/unnamed-chunk-10-1.png)

```r
# Class & NativeLanguage (density)
ggplot(lexdec_corr, aes(x = RT, col = NativeLanguage)) + 
    geom_density() + 
    facet_wrap(~ Class) + 
    theme_bw()
```

![plot of chunk unnamed-chunk-10](figure/unnamed-chunk-10-2.png)

- a Trial változó hatása

```r
# Trial
ggplot(lexdec_corr, aes(x = Trial, y = RT)) + 
    geom_point() + 
    stat_smooth(method = "lm") + 
    facet_wrap(~Subject) + 
    theme_bw()
```

![plot of chunk unnamed-chunk-11](figure/unnamed-chunk-11-1.png)


## Adatok előkészítése

- ha lennének egyértelmű outlierek, azokat érdemes az elemzés előtt kiszűrni
- standardizálhatjuk a folytonos változókat

```r
lexdec_corr[, c("scRT", "scTrial")] <- scale(lexdec_corr[, c("RT", "Trial")])
```

- az elemzési céljainktól függ, de érdemes lehet átállítani a kontrasztokat (az R alapból treatment-kontrasztot használ)

```r
op <- options(contrasts = c("contr.sum", "contr.poly"))
```



