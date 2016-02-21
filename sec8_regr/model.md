# Modellépítés

A kérdés megválaszolásához tökéletesen elég egy lineáris regressziós modellt
futtatnunk. Ezen modellben a szókincs és a csoporttagság szerepel mint
magyarázó változók (az előbbi folytonos, az utóbbi kategoriális), a függő 
változónk pedig az olvasás. 



### A modellezés előtt

Lineáris regressziós modellek futtatása előtt érdemes standardizálni a változókat, ha maguknak a regressziós együtthatóknak nincsen különösebb jelentősége számunkra. (Ettől most eltekintünk.)

Szintén érdemes lehet átállítani az R alapértelmezett
kontrasztjait ortogonális kontrasztokra.


```r
## példa összeg-kontraszt beállítására 
## (lásd ?contrasts, 'Options set in package stats' résznél)
#op <- options(contrasts = c("contr.sum", "contr.poly"))

## ha a későbbiekben vissza akarnám állítani az eredeti kontrasztokat,
## ezt a parancsot kellene megadni:
#options(op)
```


### Modell megadása

- lineáris modell futtatása:

```r
model <- lm(formula = olvasas ~ csoport * szokincs, 
            data = dat)
```

A fentebbi modellmegadási mód a `formula` interfészt használja, és kiválóan
példázza az _R_ egyik fő erősségét, a statisztikai modellek futtatásának 
viszonylag egyszerű és intuitív lehetőségét. Lássuk külön-külön az egyes 
elemeket.

- a statisztikai eljárás megadása:

```r
lm(...)
```

Jelen példában az `lm()` függvényt használjuk, amely a 'lineáris modell' rövidítése. Amennyiben a függő változónk a csoporttagság, a független változók pedig az olvasás és a szókincs lennének, a dichotóm függő változó miatt a `glm()` függvényt kellene alkalmaznunk, `family = "binomial"` argumentummal. (A `glm` az általánosított lineáris modell rövidítése, és nemcsak az imént felmerült logisztikus regressziót, hanem pl. poisson regressziót is tud futtatni.)

- a formula megadása:

```r
olvasas ~ csoport * szokincs
```

A `formula` megadásához alaposan olvassuk el a `?formula` súgóját. Röviden: a bal oldalra kerül a függő változó, majd a hullámvonal jobb oldalára a magyarázó változók. A magyarázó változók közötti operátor jelzi, hogy főhatásról vagy interakcióról van-e szó: `+`-szal elválasztott változónevek főhatásokat jelentenek, `:`-szal elválasztott változónevekkel az interakciós tagot magát (főhatások nélkül) szerepeltetjük, a `*` pedig a főhatásokat és az interakciós tagot is beleteszi a modellbe. A formulában expliciten szerepeltethetjük a konstanst is (a konstans jele: `1`); mivel az `lm` (és jellemzően a többi
modellező függvény) a konstans tagot automatikusan beleteszi a modellbe, erre
rendszerint nincsen szükség.

- a fentebbieknek megfelelően a modellünket így is megadhattuk volna:

```r
# mivel a formula az első argumentuma az lm() függvénynek (és általában a 
# modellező függvényeknek), így nem is kell külön kiírnunk
lm(olvasas ~ 1 + csoport + szokincs + csoport:szokincs, data = dat)
```

Ha a formulát közvetlenül a modellező függvényben adjuk meg (nem pedig korábban
hoztuk létre), az `lm()` függvény a formulában megadott változóneveknek megfelelő adatobjektumokat abban a környezetben fogja keresni, ahol a függvényt meghívjuk.
Ezt kerülhetjük ki a `data` argumentummal, ugyanis ha azt megadjuk, akkor a 
függvény első körben a `data` data.frame-ben keresi az adott változókat.

- vessük össze a következőket:

```r
# ez hibát eredményez, hiszen a globális környezet nem tartalmaz ilyen
# változókat
lm(olvasas ~ csoport * szokincs)
```

```
## Error in eval(expr, envir, enclos): object 'olvasas' not found
```


```r
# a 'with()' függvényt már alkalmaztuk az ábrázolásnál is; ezen 
# függvény első argumentuma a keresési út első pozíciójába helyezendő
# adatnak felel meg
with(dat, lm(olvasas ~ csoport * szokincs))
```

```
## 
## Call:
## lm(formula = olvasas ~ csoport * szokincs)
## 
## Coefficients:
##         (Intercept)           csoportsni             szokincs  
##             46.8792              29.0598               0.9497  
## csoportsni:szokincs  
##             -0.9818
```


```r
# ez pedig a leginkább áttekinthető megadási mód
lm(olvasas ~ csoport * szokincs, data = dat)
```

```
## 
## Call:
## lm(formula = olvasas ~ csoport * szokincs, data = dat)
## 
## Coefficients:
##         (Intercept)           csoportsni             szokincs  
##             46.8792              29.0598               0.9497  
## csoportsni:szokincs  
##             -0.9818
```

### A becsült paraméterek és egyéb eredmények megtekintése

- a sima `print()` parancs nem túl informatív:

```r
print(model)
```

```
## 
## Call:
## lm(formula = olvasas ~ csoport * szokincs, data = dat)
## 
## Coefficients:
##         (Intercept)           csoportsni             szokincs  
##             46.8792              29.0598               0.9497  
## csoportsni:szokincs  
##             -0.9818
```

- a `summary()` annál inkább:

```r
summary(model)
```

```
## 
## Call:
## lm(formula = olvasas ~ csoport * szokincs, data = dat)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -43.650 -18.766  -0.269  14.687  59.056 
## 
## Coefficients:
##                     Estimate Std. Error t value Pr(>|t|)   
## (Intercept)          46.8792    16.0050   2.929  0.00428 **
## csoportsni           29.0598    18.9169   1.536  0.12789   
## szokincs              0.9497     0.3663   2.593  0.01106 * 
## csoportsni:szokincs  -0.9818     0.5121  -1.917  0.05828 . 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 22.96 on 93 degrees of freedom
## Multiple R-squared:  0.1295,	Adjusted R-squared:  0.1014 
## F-statistic:  4.61 on 3 and 93 DF,  p-value: 0.004718
```

- vedd észre, hogy a `summary` eredményét ugyanúgy hozzárendelheted egy új 
objektumhoz, mint magát a modellt

```r
# a summary() valójában egy listát ad eredményül
model_sum <- summary(model)

# az egyik listaelem az együtthatók táblázatát tartalmazza,
# de ennek elérésére jobb a 'coef' függvényt használni (lásd köv. pont)
model_sum$coefficients
```

```
##                       Estimate Std. Error   t value    Pr(>|t|)
## (Intercept)         46.8792259 16.0049561  2.929044 0.004276137
## csoportsni          29.0598082 18.9168865  1.536183 0.127888712
## szokincs             0.9496837  0.3662897  2.592712 0.011059568
## csoportsni:szokincs -0.9817849  0.5120846 -1.917232 0.058277874
```

- számos egyéb olyan függvény létezik, amelyek bizonyos paraméterek kinyerését
könnyítik meg vagy az illesztett modellből, vagy a model summary-ből (lásd pl.
`?coef`, `?fitted`, `?resid`, `?vcov`)

```r
# koefficiensek
coef(model)
```

```
##         (Intercept)          csoportsni            szokincs 
##          46.8792259          29.0598082           0.9496837 
## csoportsni:szokincs 
##          -0.9817849
```

```r
# koefficiensek standard hibákkal és egyebekkel;
# itt kihasználjuk, hogy az előbb már eltároltuk a 'summary()' eredményét
coef(model_sum)
```

```
##                       Estimate Std. Error   t value    Pr(>|t|)
## (Intercept)         46.8792259 16.0049561  2.929044 0.004276137
## csoportsni          29.0598082 18.9168865  1.536183 0.127888712
## szokincs             0.9496837  0.3662897  2.592712 0.011059568
## csoportsni:szokincs -0.9817849  0.5120846 -1.917232 0.058277874
```

### Több modell összehasonlítása

Gyakori modellezési taktika, hogy beágyazott modelleket építünk, és (a 
becsült paraméterek számával korrigáltan) legjobban illeszkedő modellt 
keressük. A fentebbi példa eredményeiben például nem elég meggyőző a csoport
hatása; vizsgáljuk meg a csoport interakciós és főhatásának elhagyásával 
kapott modellek illeszkedését.

- a fentebbi példa lehetséges egyszerűsítései:

```r
# interakció nélkül
model_no_ia <- lm(olvasas ~ csoport + szokincs, data = dat)

# főhatás és interakció nélkül
model_no_group <- lm(olvasas ~ szokincs, data = dat)
```

- a modellek összehasonlítása:

```r
anova(model_no_group, model_no_ia, model)
```

```
## Analysis of Variance Table
## 
## Model 1: olvasas ~ szokincs
## Model 2: olvasas ~ csoport + szokincs
## Model 3: olvasas ~ csoport * szokincs
##   Res.Df   RSS Df Sum of Sq      F  Pr(>F)  
## 1     95 51336                              
## 2     94 50976  1    359.96 0.6827 0.41079  
## 3     93 49038  1   1938.19 3.6758 0.05828 .
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

- modellek összehasonlítása AIC kritériummal:

```r
AIC(model_no_group, model_no_ia, model)
```

```
##                df      AIC
## model_no_group  3 889.6030
## model_no_ia     4 890.9204
## model           5 889.1604
```


