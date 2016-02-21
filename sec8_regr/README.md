# ANOVA és regressziós modellek

A regressziószámítás során egy függő változó értékét próbáljuk bejósolni
egy vagy több magyarázó változó értéke alapján. Amennyiben a magyarázó változók
és a függő változó kapcsolatát lineáris összefüggéssel próbáljuk leírni, 
lineáris regressziószámításról beszélünk. A pszichológusok körében
talán jobban ismert varianciaanalízis is a regressziószámítás egyik speciális 
esete, amelyben a magyarázó változóink kategoriális változók. 

Az R-ben a lineáris regresszió alapfüggvénye az `lm` függvény. Tulajdonképpen
erre a függvényre épül a varianciaanalízist lehetővé tevő `aov` függvény. 
Varianciaanalízisre azonban alkalmasabb az *ez* package `ezANOVA` függvénye,
ezért a későbbiekben azt fogjuk tárgyalni az `aov` függvény helyett.

Egy regressziószámítás (és gyakorlatilag akármilyen statisztikai modellezés) a 
következő lépésekből áll:

1. Adatok explorációja (leíró statisztikák, ábrázolás)
2. Modellépítés és -illesztés
3. Eredmények ellenőrzése és értelmezése

A következőkben tehát ezen főbb lépéseket mutatjuk be a korábban már 
megismert olvasásfejlődési adatok elemzésén keresztül. Az alapkérdésünk a következő: a 2-4 osztályos tanulók körében bejósolja-e az olvasási teljesítményt
a tanuló szókincse, illetve csoporttagsága (kontroll/SNI)?

* [Leíró statisztikák](descr.md)
* [Modellépítés](model.md)
* [Ellenőrzés](checkmodel.md)
* [ANOVA: Az 'ez' csomag](ez.md)
