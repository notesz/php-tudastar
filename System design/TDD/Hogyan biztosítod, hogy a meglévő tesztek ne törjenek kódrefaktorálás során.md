A kódrefaktorálás során a meglévő tesztek épségének megőrzéséhez több fontos lépést és technikát érdemes alkalmazni:

## Alapos tesztkészlet kialakítása

Mielőtt elkezdenénk a refaktorálást, fontos, hogy rendelkezzünk egy átfogó tesztkészlettel:

- Írjunk egységteszteket a meglévő kódhoz, ha még nincsenek.
- Győződjünk meg róla, hogy a tesztek lefedik a refaktorálandó területeket.
- Használjunk kód lefedettség mérő eszközöket (pl. Xdebug, PHPUnit beépített funkciója) a tesztek minőségének ellenőrzésére.

## Fokozatos megközelítés

- Alkalmazzunk kis lépéseket a refaktorálás során.
- Minden egyes refaktorálási lépés után futtassuk le a teszteket.
- Ideális esetben csak egyetlen refaktorálási műveletet végezzünk el egyszerre (pl. metódus kiemelése, változó átnevezése).

## Automatizálás és reprodukálhatóság

- Állítsunk fel egy automatizált rendszert a fejlesztői környezet visszaállítására (pl. adatbázis reset).
- Biztosítsuk, hogy a tesztek konzisztensen futnak, függetlenül a külső tényezőktől (pl. dátum-függő teszteknél).

## Tesztek karbantartása

- Ne feledkezzünk meg a tesztkód refaktorálásáról sem.
- A tesztek refaktorálása során használjuk az alkalmazás kódját a tesztek helyességének ellenőrzésére.

## További technikák

- Használjunk verziókezelő rendszert és commitoljunk gyakran, minden sikeres tesztfuttatás után.
- Fontoljuk meg magasabb szintű funkcionális tesztek írását (pl. Mink használatával) a teljes alkalmazás viselkedésének ellenőrzésére.

A kulcs a fokozatosság és a folyamatos tesztelés. Minél kisebb lépésekben haladunk és minél gyakrabban futtatjuk a teszteket, annál nagyobb eséllyel tudjuk megelőzni a tesztek törését és biztosítani a refaktorálás sikerességét.