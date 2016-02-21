# Az R és az RStudio IDE telepítése

- az alábbiak nem keverendők:    
    - az R magának a programnyelvnek a neve    
    - a CRAN (Comprehensive R Archive Network) tulajdonképpen ftp- és webszerverek
hálózata, amely az R nyelv kódjának verzióit és dokumentációját tárolja     
        - egy-egy "mirror" tulajdonképpen ezen gyűjtemény egy-egy klónja     
        - a magyarországi mirror-t a Rapporter cég biztosítja a 
http://cran.rapporter.net címen      
        - a CRAN mellett egyéb más "hivatalos" és "nem hivatalos" repozitórium létezik (pl. [Bioconductor](http://www.bioconductor.org/), ill. a nem R-specifikus, Git alapú hosting szolgáltatás, a [GitHub](https://github.com/))
    - minden programnyelvre igaz, hogy jellemzően IDE-ben (Integrated Developmental
Environment), azaz integrált fejlesztői környezetben folyik az alkalmazások 
fejlesztése      
        - az R legnépszerűbb IDE-jét ([RStudio IDE](https://www.rstudio.com/products/RStudio/)) az RStudio nevű cég fejleszti     
        - emellett sok más IDE is használható (a legerőteljesebb az Emacs editorra 
épülő [ESS](http://ess.r-project.org/)), de ha Windows-t használsz, érdemes
lehet telepíteni akár a [Notepad++](https://notepad-plus-plus.org/) szerkesztőt 
is az [NppToR](http://sourceforge.net/projects/npptor/) pluginnal 
        - az RGui-t (azt a programocskát, amelyik a Windows-os változathoz
        alapból jár) csak akkor használd, ha nagyon-nagyon muszáj, vagy ha 
        büntetni akarod magad

### Az R telepítése

- az R központi oldalának címe: https://www.r-project.org/
- válaszd ki a tartózkodási helyedhez legközelebbi mirror-t, és az operációs
rendszerednek megfelelően telepítsd a "precompiled binary" disztribúciót
    - ha Windows-t használsz, az [alapváltozaton](http://cran.rapporter.net/bin/windows/base/) felül érdemes 
telepítened az [Rtools](http://cran.rapporter.net/bin/windows/Rtools/) legújabb
változatát is     

### Az RStudio telepítése és használata

- az RStudio telepítése szintén rém egyszerű; telepítsd az operációs rendszerednek
megfelelő legújabb [stabil](https://www.rstudio.com/products/rstudio/download/) vagy a többnyire újabb funkciókkal gazdagított, de
kevésbé stabil [fejlesztői](https://www.rstudio.com/products/rstudio/download/preview/) változatot
- az RStudio nagyon intuitíven használható, de érdemes rászánni az időt a súgó (Help/RStudio Docs) tanulmányozására
- a kurzus során az RStudio-t fogjuk használni, így a legfontosabb funkciókat 
(néhány kényelmi tipp-pel együtt) menet közben bemutatom

![Az RStudio kezelőfelülete (példa)](/images/rstudio.png)

- a két legfontosabb ablak (pane) a Console és a Source:
    - a Console (magyarul konzol, vagy bővebben parancssoros felhasználói 
    felület) az a felület, ahová beírt parancsokat az R lefuttatja -> valós
    adatelemzés esetén ide közvetlenül nem gépelünk parancsokat, kivéve néhány
    triviális esetet
    - a Source (forráskód, szkript-ablak) az a felület, ahová az általunk 
    definiált függvények programkódját, illetve egy adatelemzés során
    futtatni kívánt parancsokat írjuk (a függvényeket és az adatelemzési 
    lépéseket érdemes külön fájlokban tárolni) -> a Source ablakban írt 
    fájlok valójában egyszerű szövegfájlok, azaz pl. Notepad-ben is megírhatók
    vagy szerkeszthetők lennének (csak jellemzően sokkal kényelmetlenebbül)
    - a jellemző módszer: megírod a parancsokat a szerkesztőben, majd kijelölöd
    a futtatni kívánt sorokat, és rákattintasz a Run gombra (vagy a Run helyett
    használod a Ctrl+Enter billentyűkombinációt)
- valódi adatelemzést MINDIG Project keretében végezz (lásd File / New Project)


