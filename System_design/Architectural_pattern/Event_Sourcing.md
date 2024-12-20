# Event Sourcing

Az Event Sourcing egy szoftverarchitektúrális tervezési minta, amely az alkalmazás állapotváltozásait események sorozataként tárolja el. Ahelyett, hogy csak a legfrissebb állapotot rögzítené, az Event Sourcing az összes változás történetét megőrzi.

## Főbb jellemzők

- **Események mint igazságforrás**\
Minden állapotváltozást egy esemény reprezentál, amely immutábilis és szekvenciálisan tárolódik egy eseménytárban.

- **Append-only tárolás**\
Az események egy csak hozzáfűzéses (append-only) adatbázisban kerülnek tárolásra, ahonnan nem lehet törölni őket.

- **Állapot rekonstrukció**\
Az alkalmazás aktuális állapota az események visszajátszásával bármikor rekonstruálható.

## Előnyök

1. **Teljes auditálhatóság**\
Minden változás nyomon követhető, ami kiváló auditálási lehetőségeket biztosít.

2. **Időutazás**\
Lehetővé teszi az alkalmazás korábbi állapotainak rekonstruálását bármely időpontban.

3. **Fejlett analitika**\
Egyedi adatreprezentációk (projekciók) generálhatók a historikus adatok lekérdezéséhez és minták azonosításához.

4. **Skálázhatóság**\
Az események aszinkron módon kezelhetők, ami javíthatja a teljesítményt és a skálázhatóságot.

5. **Gazdag adatkészlet**\
Az események üzleti döntéseket és tényeket tükröznek, ami értékes betekintést nyújt.

## Event Sourcing a gyakorlatban

Az Event Sourcing egy olyan szoftverarchitektúrális megközelítés, amely az alkalmazás állapotváltozásait események sorozataként tárolja el. A gyakorlatban ez a következőképpen működik:

## Események rögzítése

- Minden állapotváltozást egy esemény reprezentál, például "RendelésFelvéve" vagy "FizetésMegérkezett"[1].
- Az események immutábilisak és szekvenciálisan tárolódnak egy csak hozzáfűzéses (append-only) adatbázisban, amit eseménytárnak nevezünk[3].

## Állapot rekonstrukció

- Az alkalmazás aktuális állapota az események visszajátszásával bármikor rekonstruálható[1].
- Ez történhet igény szerint, például amikor egy kérés kezeléséhez szükség van egy tartományi objektumra, vagy ütemezett tevékenységként a materializált nézetek frissítéséhez[3].

## Gyakorlati példa

Az Event Sourcing gyakran együtt használatos a CQRS (Command Query Responsibility Segregation) mintával

Vegyünk egy egyszerű helyfoglaló rendszert:

1. Amikor egy felhasználó lefoglal egy helyet, egy "HelyLefoglalva" esemény kerül az eseménytárba.
2. Ha a foglalást lemondják, egy "FoglalásLemondva" esemény kerül rögzítésre.

Ahelyett, hogy közvetlenül módosítanánk egy táblát a foglalások aktuális állapotával, az eseményeket tároljuk, és ezekből építjük fel a rendszer állapotát.

Így minden változás nyomon követhető, hiszen az összes esemény megőrződik Illetve az események aszinkron módon kezelhetők.