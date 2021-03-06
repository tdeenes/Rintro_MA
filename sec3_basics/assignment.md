# R objektumok létrehozása

Egy példa: számítsuk ki, hogy mennyi 3 + 4.

```r
3 + 4
```

```
## [1] 7
```

Valójában az SPSS és számos kommerciális statisztikai program a felhasználó
szempontjából nem több egy nagyon bonyolult számológépnél: megadod az inputokat,
az inputok közötti műveleteket, majd a program kiprinteli az eredményt. Az R ennél jóval több: itt minden input és művelet valójában egy objektum, és a műveletek eredménye szintén egy objektum. Ez azért nagyon klassz, mert ezáltal egy eredményt
felhasználhatsz egy másik művelet inputjaként, illetve a műveleteket is kombinálhatod. Ha egy művelet eredményét meg akarod "őrizni" későbbi felhasználásra, azt jelezned kell az R-nek. 

Az R-ben számos módon létrehozhatunk objektumokat, ezek közül a legalapvetőbb
a `<-` jel (amely valójában egy függvény, lásd később).

- `<-` a hozzárendelés jele

```r
x <- 3 + 4
```

- ha ki akarod íratni egy objektum tartalmát:

```r
# ha konzolban vagy, ez automatikusan 
# meghívja a print parancsot
x
```

```
## [1] 7
```

```r
# függvényen belül expliciten ki kell 
# írni a print parancsot
print(x) 
```

```
## [1] 7
```

```r
# sima zárójel (függvény nélkül) szintén a 
# print-et hívja meg; ezt valódi elemzéseknél 
# ne használd, de oktatási anyagban jól jön
(x <- 3 + 4) 
```

```
## [1] 7
```

- az `=` szintén használható hozzárendelésre, de inkább korlátozzuk függvényargumentumok megadására (lásd később)

- FONTOS: az objektumok neve ne tartalmazzon ékezetes betűket, ne *kezdődjön* számmal vagy speciális karakterrel (pl.: _), és nem árt, ha a név tükrözi az objektum tartalmát, sőt, esetleg az objektum jellegét is (pl. függvény vagy változó)

