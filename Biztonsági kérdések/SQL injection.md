Az SQL injection egy veszélyes biztonsági sebezhetőség, amely lehetővé teszi a támadók számára, hogy rosszindulatú SQL utasításokat futtassanak egy adatbázis-vezérelt alkalmazásban. Íme a legfontosabb tudnivalók erről a támadási módszerről:
## Az SQL injection működése

- A támadó speciálisan kialakított adatokat ad meg egy alkalmazás beviteli mezőjében (pl. bejelentkezési űrlap, keresőmező).
- Ezek az adatok úgy vannak megformálva, hogy módosítsák vagy kiegészítsék az eredeti SQL lekérdezést.
- Ha az alkalmazás nem megfelelően kezeli a felhasználói bevitelt, a rosszindulatú kód végrehajtódik az adatbázison.
## Következmények

Az SQL injection támadások lehetővé tehetik a támadók számára, hogy:

- Hozzáférjenek érzékeny adatokhoz
- Módosítsák vagy töröljék az adatbázis tartalmát
- Adminisztrátori jogosultságokat szerezzenek
- Teljes hozzáférést nyerjenek az adatbázisszerverhez
## Védekezési módszerek

1. Prepared statement használata paraméterezett lekérdezésekkel
2. Megfelelően kialakított tárolt eljárások alkalmazása
3. Bemeneti adatok szigorú ellenőrzése és szűrése
4. Az alkalmazás és az adatbázis-felhasználó jogosultságainak minimalizálása

Bővebben a prepared statement-ről:
[[Mi a prepared statement és miért fontos használni?]]

Az SQL injection elleni védekezés kulcsfontosságú a webalkalmazások biztonságának megőrzésében. A fejlesztőknek mindig ügyelniük kell arra, hogy megfelelően kezeljék a felhasználói bevitelt, és alkalmazzák a bevált biztonsági gyakorlatokat az adatbázis-lekérdezések során.
## Az SQL injection egy gyakorlati példája

Egy sikeres SQL-injekció a következőképpen működik:
### A támadás folyamata

1. **Sebezhető pont azonosítása**: A támadó olyan beviteli mezőket keres az alkalmazásban, amelyek nem megfelelően kezelik a felhasználói inputot. Ezek lehetnek bejelentkezési űrlapok, keresőmezők vagy URL-paraméterek.

2. **Rosszindulatú SQL-kód készítése**: A támadó olyan SQL-utasítást készít, amely módosítja az eredeti lekérdezést. Például egy bejelentkezési űrlapnál:

   Eredeti lekérdezés:
   ```sql
   SELECT * FROM users WHERE username='$username' AND password='$password'
   ```
   
   Támadó által módosított lekérdezés:
   ```sql
   SELECT * FROM users WHERE username='admin'--' AND password='bármi'
   ```
   
   Itt a `--` kommentárként működik, így a jelszó ellenőrzése kimarad.

3. **Biztonsági intézkedések megkerülése**: A támadó olyan technikákat alkalmaz, mint a string összefűzés vagy SQL-szintaxis használata kommentárok létrehozására, hogy megkerülje az alkalmazás biztonsági ellenőrzéseit.

4. **Rosszindulatú lekérdezés végrehajtása**: Az alkalmazás végrehajtja a módosított SQL-lekérdezést, amely tartalmazza a támadó által beszúrt kódot.

5. **Adatok kinyerése vagy manipulálása**: A sikeres támadás eredményeként a támadó:
   - Hozzáférhet érzékeny adatokhoz
   - Módosíthatja vagy törölheti az adatbázis tartalmát
   - Adminisztrátori jogosultságokat szerezhet
   - Teljes hozzáférést nyerhet az adatbázisszerverhez

## Az alkalmazás tesztelése

Az SQL-injekció felfedezése egy webalkalmazásban több módszerrel is lehetséges. Íme néhány hatékony technika:
### Manuális tesztelés

**Szisztematikus beviteli tesztek**:

- Egyszerű karakterek, mint az aposztróf (') beillesztése és a hibaüzenetek figyelése.
- SQL-specifikus szintaxis használata, amely az eredeti értéket és egy módosított értéket ad vissza.
- Logikai feltételek (pl. OR 1=1, OR 1=2) tesztelése és a válaszok eltéréseinek vizsgálata.
- Időkésleltetést okozó lekérdezések (pl. SLEEP() függvény) használata.

**Különböző részek tesztelése**:

- WHERE záradékok vizsgálata SELECT utasításokban.
- UPDATE utasítások frissített értékeinek és WHERE záradékainak ellenőrzése.
- INSERT utasítások beszúrt értékeinek vizsgálata.
- SELECT utasítások tábla- és oszlopneveinek tesztelése.
- ORDER BY záradékok ellenőrzése SELECT utasításokban.
### Automatizált eszközök használata

Ilyen eszközök például:
- [[SQLMap]]
- Burp Scanner
- OWASP ZAP
### Monitorozás és naplózás

- Valós idejű adatbázis-tevékenység figyelése.
- Szokatlan viselkedések és anomáliák azonosítása.
- HTTP-forgalom elemzése SQL-töredékek után kutatva.
- Adatbázis-hibák monitorozása.
### Web Application Firewall (WAF) használata

A WAF-ok képesek szűrni és blokkolni a gyanús SQL-lekérdezéseket tartalmazó HTTP-kéréseket.