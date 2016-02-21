# Interaktív vizualizáció

Az R interaktív vizualizációs képessége jelentősen elmarad a statikus 
ábrázolási képességétől, de az utóbbi időben ezen a téren is jelentős fejlődés tapasztalható. Idő hiányában csak rövid felsorolást adok arról, hogy milyen
csomagoknak érdemes utánanézned:

- [iplots](https://cran.r-project.org/web/packages/iplots/index.html): interaktív, összekapcsolt scatterplot, barplot, mosaicplot stb., 
adatexplorációs célra kiváló (ezzel kapcsolatban vess egy pillantást a [Deducer GUI](http://www.deducer.org/)-ra is)
- [playwith](https://cran.r-project.org/web/packages/playwith/index.html): ha módosítgatni akarod az ábrádat, interaktívan megteheted
- [rCharts](http://rcharts.io/): javascript könyvtárakra épül, egész jól használható
- [htmlwidgets](http://www.htmlwidgets.org/): ez az a csomag, amely forradalmasította az interaktív JavaScript vizualizációs könyvtárak integrációját az R-be. Látogass el [ide](http://www.buildingwidgets.com/blog), hogy ez mi 
mindent jelenthet. Ha nagyméretű idősorokkal dolgozol (pl. EEG), akkor nagyon
hasznosnak fogod találni pl. a *dygraphs* csomagot.
- [rgl](https://cran.r-project.org/web/packages/rgl/index.html): 3D ábrázoláshoz, nagyon gyors és nagyon klassz
- [ggvis](http://ggvis.rstudio.com/): a ggplot2-re hasonlít, de egyelőre még gyerekcipőben jár
- további csomagok: animate, manipulate

Végül ha érdekel az interaktív adatelemzés, feltétlenül próbáld ki a [Shiny](http://shiny.rstudio.com/)-t. Ez a csomag (valójában inkább keretrendszer) nem csupán interaktív ábrázolást tesz lehetővé, hanem webes GUI-t hozhatsz létre 
vele anélkül, hogy bármit is értenél a webes programozáshoz.
