# XSS (Cross-Site Scripting)

Az XSS (Cross-Site Scripting) egy elterjedt biztonsági sebezhetőség, amely a webalkalmazásokban fordul elő. Lényege, hogy a támadó rosszindulatú kódot, általában JavaScript szkriptet injektál egy megbízható weboldalba, amelyet aztán a gyanútlan felhasználók böngészője végrehajt.

## XSS támadások típusai

1. Tárolt (perzisztens) XSS: A támadó által beszúrt rosszindulatú kód tartósan tárolódik a célalkalmazásban, például egy adatbázisban. Amikor egy felhasználó megnyitja az érintett weboldalt, a kártékony szkript a HTML-kóddal együtt kerül kiszolgálásra.

2. Reflected (nem perzisztens) XSS: A támadó által készített payload a szervernek küldött kérés részét képezi, majd onnan visszatükröződik a válaszban. A támadók gyakran használnak rosszindulatú linkeket vagy adathalász e-maileket, hogy rávegyék az áldozatot a kérés elküldésére.

3. DOM-alapú XSS: Ez egy fejlettebb XSS-támadás, ahol a webalkalmazás kliens oldali szkriptjei írják be a felhasználó által megadott adatokat a Document Object Model-be (DOM). Ha az adatkezelés nem megfelelő, a támadó olyan payloadot injektálhat, amely a DOM részeként tárolódik és végrehajtódik.

Az XSS-támadások veszélyesek, mert lehetővé teszik a támadók számára, hogy megkerüljék az azonos eredetű házirendet, amely a különböző webhelyek elkülönítésére szolgál. A támadók így hozzáférhetnek érzékeny adatokhoz, ellophatják a munkamenet-sütiket, és az áldozat nevében hajthatnak végre műveleteket.

## Védekezés

Az XSS (Cross-Site Scripting) elleni védekezés több rétegű megközelítést igényel. Íme néhány hatékony módszer az XSS támadások megelőzésére:

### Bemeneti adatok validálása és szanitizálása

- Minden felhasználói bemenetet szigorúan ellenőrizni kell.
- A bemeneti adatokat megfelelően kell szanitizálni, mielőtt azok bekerülnének az adatbázisba vagy megjelennének a weboldalon.
- Használjunk speciális függvényeket vagy könyvtárakat a szanitizáláshoz, például a PHP htmlspecialchars() függvényét.

### Kimeneti kódolás

- A dinamikusan generált tartalmakat mindig kódolni kell, mielőtt azok megjelennének a weboldalon.
- Használjunk kontextus-specifikus kódolást (HTML, JavaScript, CSS, URL).

### Content Security Policy (CSP) használata

- A CSP egy hatékony biztonsági réteg, amely korlátozza, hogy milyen erőforrásokat tölthet be és futtathat a böngésző.
- Megfelelően konfigurált CSP segíthet megakadályozni az XSS támadásokat.

### HttpOnly és Secure flag használata a sütikben

- Az HttpOnly flag megakadályozza, hogy a JavaScript hozzáférjen a sütikhez.
- A Secure flag biztosítja, hogy a sütik csak HTTPS kapcsolaton keresztül kerüljenek továbbításra.

### Keretrendszerek és könyvtárak használata

- Használjunk olyan modern keretrendszereket és könyvtárakat, amelyek beépített XSS védelemmel rendelkeznek.
- Például a React automatikusan escapeli a beágyazott értékeket.

### Rendszeres biztonsági auditok és penetrációs tesztek

- Rendszeresen ellenőrizzük az alkalmazást XSS sebezhetőségek szempontjából.
- Használjunk automatizált szkennelő eszközöket és végezzünk manuális teszteket is.