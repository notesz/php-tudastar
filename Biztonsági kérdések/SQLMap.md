A SQLMap egy hatékony, nyílt forráskódú eszköz az SQL-injekciós sebezhetőségek felderítésére és kihasználására.
[sqlmap.org](https://sqlmap.org)

Az SQLMap működése az SQL-injekció felismerésében:
## Automatikus sebezhetőség-felismerés

A SQLMap képes automatikusan felismerni a potenciálisan sebezhető célpontokat. Ez azt jelenti, hogy még ha nem is vagyunk biztosak abban, mely paraméterek sebezhetőek, a SQLMap intelligensen átvizsgálja a célpontot és azonosítja a lehetséges injekciós pontokat[1].

## Különböző technikák alkalmazása

A SQLMap több SQL-injekciós technikát is támogat:

- **Boolean-alapú vak SQL-injekció**: A SQLMap olyan payloadokat küld, amelyek igaz vagy hamis feltételt eredményeznek az SQL-lekérdezésben, és figyeli az alkalmazás viselkedésének változásait.

- **Időalapú vak SQL-injekció**: Az eszköz olyan payloadokat küld, amelyek időkésleltetést okoznak a szerver válaszában, például a SLEEP() függvény használatával.

- **Hibaüzenet-alapú SQL-injekció**: A SQLMap olyan payloadokat injektál, amelyek adatbázis-hibákat generálnak, és az ezekben visszaadott információkat használja fel.

- **UNION-alapú SQL-injekció**: Az eszköz azonosítja az oszlopok számát, és a UNION operátort használja adatok kinyerésére más táblákból.

## Adatbázis-felderítés

A SQLMap képes adatbázis- és táblaséma-információk lekérésére. Ez lehetővé teszi a tesztelők számára, hogy értékes betekintést nyerjenek a célzott adatbázis szerkezetébe, beleértve a táblák, oszlopok neveit és azok adattípusait.

## Automatizált kihasználás

A sebezhetőség felismerése után a SQLMap automatikusan megkezdi a kihasználási folyamatot, kinyerve a kívánt információkat az adatbázisból.

A SQLMap hatékony eszköz az SQL-injekciós sebezhetőségek felderítésére, de fontos megjegyezni, hogy használata csak megfelelő engedéllyel és etikus keretek között legális.