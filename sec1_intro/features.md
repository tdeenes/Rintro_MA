# Az R főbb jellegzetességei

- magas szintű, interpretált programnyelv (mint pl. a Python vagy a Matlab)
- alapesetben mindent a memóriában (RAM-ban) tárol (és jellemzően nem túl hatékonyan), de ezen a hiányosságon számos csomag segíthet (lásd a vonatkozó [TaskView-t](http://cran.r-project.org/web/views/HighPerformanceComputing.html))
- helyes kódolással (vektorizált fv-eket használva) elfogadhatóan gyors
- nagyon sok interface létezik az R és egyéb külső szoftverek/programnyelvek
között (pl. R & C++, R & Python, R & Matlab, R és MySQL/SQLite/Oracle/JSON/...)
- csak néhány "beépített" csomagot tartalmaz, de korlátlanul bővíthető
    - egy csomag (package) tulajdonképpen nem más, mint az R "beépített" függvényeit,
    adatkészleteit és dokumentációját kiegészítő, jellemzően egy-egy statisztikai 
    vagy adatkezelési probléma köré épülő függvények, adatkészletek és ezek 
    dokumentációinak együttese
    - bárki írhat R-csomagot, és ezt szabadon megoszthatja a közösséggel

### Az R legfőbb erényei
- extrém módon támogató közösség (általános és speciális levlisták, useR csoportok, lásd pl. [BURN](http://www.meetup.com/Budapest-Users-of-R-Network/) :)
- kiváló grafikai képességek, rendkívül gazdag ábrázolási lehetőségek
- szinte minden statisztikai módszerre vagy létezik csomag, vagy csak ki kell várnod, hogy valaki implementálja
- rendkívül egyszerűen bővíthető
- interaktív, rugalmas adatelemzésre kiemelten alkalmas
