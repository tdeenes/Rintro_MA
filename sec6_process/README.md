# Adatfeldolgozás

Ritka az a helyzet, amikor az adatok beolvasását követően azonnal hozzá
láthatunk az adatok elemzéséhez. Többnyire szükség van a megfigyelési 
egységeinek vagy a változóink szűrésére (szelekciójára), a változók 
transzformációjára vagy az adattáblánk egyéb átalakítására. A következőkben csak
azzal a leggyakoribb esettel foglalkozunk, amikor az adataink `data.frame`-ként
állnak rendelkezésre.

Egy olvasásvizsgálati eredményeket tartalmazó adattáblát fogunk használni. 
Az adattábla kisiskolásokkal végzett felmérés eredményeit tartalmazza. A 
vizsgálatokat normál és speciális nevelési igényű gyerekkel (csoport: 0 / 1) 
végezték. Dokumentálták a gyerek nemét (1-fiú, 2-lány), korát (hónapokban mérve) 
és osztályát. Felvettek a szülőkkel egy olyan kérdőívet, amely a gyerek 
figyelemzavarának mértékét jelzi. (70 vagy afölötti érték esetén a gyerek 
figyelemzavarosnak tekinthető.) Mérték a gyerekek szókincsét, olvasási tempóját 
gyakori szavak (olv_helyes1), ritka szavak (olv_helyes2) és álszavak 
(olv_helyes3) olvasásakor, illetve helyesírásukat különböző típusú szólisták 
segítségével (sp_helyes1, sp_helyes2...).

* [Szűrés és összegzés](filter_select.md)
* [Darabolás és egyesítés](split_merge.md)
* [Átstrukturálás](reshape.md)
* [Változók átalakítása](convert.md)

