Az IDOR (Insecure Direct Object Reference) egy olyan hozzáférés-vezérlési sebezhetőség, amely akkor fordul elő, amikor egy alkalmazás közvetlenül használja a felhasználó által megadott adatokat objektumok eléréséhez anélkül, hogy megfelelő jogosultság-ellenőrzést végezne.
## Hogyan működik?

- Az alkalmazás közvetlen hivatkozást használ objektumokra (pl. adatbázis-rekordok, fájlok) URL-ekben vagy paraméterekben.
- A felhasználó módosíthatja ezeket az azonosítókat más objektumok eléréséhez.
- Az alkalmazás nem ellenőrzi megfelelően, hogy a felhasználónak van-e jogosultsága az adott objektum elérésére.
## Példák IDOR sebezhetőségre

1. URL-ben lévő azonosító módosítása:
   ```
   https://example.com/users/123
   ```
   Ha a felhasználó megváltoztatja a 123-at 124-re, és hozzáfér egy másik felhasználó adataihoz, az IDOR sebezhetőség.

2. Rejtett mezők manipulálása űrlapokon:
   ```html
   <input type="hidden" name="user_id" value="12345">
   ```
   Ha a támadó módosítja ezt az értéket, más felhasználók profiljait is frissítheti.

## Következmények

- Horizontális jogosultság-eszkaláció: Hozzáférés más, azonos jogosultságú felhasználók adataihoz.
- Vertikális jogosultság-eszkaláció: Ritkább esetben magasabb jogosultságok megszerzése.

Az IDOR sebezhetőségek komoly biztonsági kockázatot jelentenek, és megfelelő hozzáférés-vezérlési mechanizmusok implementálásával, valamint alapos teszteléssel lehet ellenük védekezni.