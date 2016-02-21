# R programozás - esettanulmány

Ebben a fejezetben egy kérdőíves vizsgálat adatait dolgozzuk fel. Az adatokat
a "data" könyvtár "gaming_random.sav" fájlja tartalmazza (SPSS adatfájl). Az elemzési
lépések bemutatása előtt közöljük a vizsgálat és a feladat leírását.

> FIGYELEM! Egy valódi vizsgálatból származó, de 
> randomizált adatokkal fogunk dolgozni. Az 
> eredményeket tehát semmiképpen ne interpretáljátok 
> úgy, mintha az valódi összefüggésekre vagy 
> különbségekre mutatna rá.

## A vizsgálat
A vizsgálat résztvevői (kb. 5200 fő) egy gaming magazin facebook-os csoportjának követői közül kerültek ki. A vizsgálat célja annak feltárása volt, hogy a sokat játszók és a problémás játékosok hogyan térnek el egymástól a pszichopatológia, játékmotivációk valamint a függőségi tünetprofil alapján. A kutatók a játékmotivációt, a problémás játékhasználatot (játékfüggőséget) és a tüneteket egy-egy kérdőívvel
vizsgálták (MOGQ: játékmotiváció, 27 item; POGQ: játékfüggőség, 18 item; 
BSI: Derogatis-féle rövid tünetskála, 53 item). Két további kérdőív alapján 
mérték a játékhasználat időtartamát és a problémás játékhasználatot, amely 
kérdőívekkel azonosíthatták a sokat játszók, illetve a problémás játékosok csoportját.

## Adatbázis
Az adatbázis két változója kódolja a sokat játszókat, illetve a problémás játékosokat:
- Sokat játszók = napi 4 órát vagy annál többet játszók
    - oszlopnév: Heavy_use  
    - szintek: 0 (4 óránál kevesebbet) és 1 (4 óránál többet játszók)]
- Problémás játékosok = IGD kérdőív (DSM-5 kritériumok) alapján cut-off feletti pontszámot elérők
    - oszlopnév: Problematic  
    - kétértékű: 0 (=nonproblematic), 1 (=problematic)

## Előkészítő műveletek

Az elemzéseket nem az egyedi itemeken, hanem az egyes kérdőívek skálapontszámain kell végezni. Az MOGQ kérdőív 7, a POGQ 6, a BSI pedig 9+1 skálából áll. Ezen
skálák számítási módját a "data" könyvtárban található, SPSS syntaxból kimásolt 
dokumentum tartalmazza ("gaming_skalak.txt"). A syntax hibás abban a 
tekintetben, hogy nem foglalkozik az esetleges hiányzó értékekkel. Kiegészítő
információként azt az instrukciót kaptuk, hogy valójában a skálákat a syntaxban megadott, érvényes értékkel rendelkező itemek átlagpontszámaként kell számolni.
További lényeges információ, hogy a számításokat a *standardizált* 
skálapontszámokon kell végezni. 

## Alkalmazandó statisztikai eljárás

A vizsgálatvezetők egy olyan ANOVA-elemzéshez ragaszkodnak, amelyben független
változóként a csoportosító szempontok (Heavy_use és Problematic) főhatásai és interakciója szerepel, függő változóként pedig valamennyi MOGQ, POGQ és BSI 
skála (mindegyik skála külön-külön). Összességében tehát `7 + 6 + 10 = 23` 
ANOVA-t kell futtatnunk.

Fontos megjegyeznünk, hogy ilyen jellegű vizsgálati adatok elemzésére valószínűtlen, hogy 23 ANOVA futtatása lenne az ideális megoldás. Önmagában problémás a csoportosító változónk képzése, (látni fogjuk, hogy) nagyon egyenlőtlen a csoportok elemszáma, várhatóan padlóhatást fogunk találni a BSI skálákon a kontrollként szolgáló csoportokban, és a 23 ANOVA független illesztése miatt rendkívül megemelkedik az elsőfajú hiba valószínűsége. Arra a célra azonban tökéletes ez a vizsgálat, hogy egy elemzés automatizálásának lehetőségét illusztráljuk vele. 

## Ábrázolás

A vizsgálatvezetők az ANOVA-eredmények mellett egy-egy ábrát kérnek a becsült
csoportátlagokról, minden egyes kérdőívre (MOGQ, POGQ, BSI) külön-külön. Az 
ábrákon az `x` tengelyen az adott kérdőív askálái szerepeljenek, és a négy
alcsoportot (2x2) különböző szín kódolja. 
