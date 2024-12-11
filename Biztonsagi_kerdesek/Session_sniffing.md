# Session sniffing

A session sniffing, más néven munkamenet-szimatolás, egy olyan támadási módszer, amely során a támadó passzívan figyeli a hálózati forgalmat, hogy elfogja a felhasználók munkamenet-adatait. Íme, hogyan működik ez a folyamat:

## A session sniffing működése

**Hálózati forgalom megfigyelése**: A támadó olyan eszközöket használ, mint például a Wireshark vagy a Kismet, amelyek lehetővé teszik számára a hálózati forgalom monitorozását. Ez különösen hatékony nem titkosított kapcsolatokon, például nyilvános Wi-Fi hálózatokon.

**Titkosítatlan adatok elfogása**: A támadó olyan munkamenet-adatokat keres, amelyeket nem titkosítottak megfelelően. Ez gyakran előfordul, ha a szerver csak a hitelesítési oldalt titkosítja, de a munkamenet többi oldalát nem.

**Munkamenet-tokenek azonosítása**: A támadó a elfogott adatokban azonosítja a munkamenet-tokeneket vagy sütiket, amelyeket a felhasználó hitelesítés után kap.

**Adatok felhasználása**: Az elfogott munkamenet-adatokkal a támadó képes lehet átvenni a felhasználó munkamenetét, és az ő nevében tevékenykedni az alkalmazásban.

## Fontos tudnivalók

- A session sniffing egy passzív támadási forma, ami azt jelenti, hogy a támadó nem módosítja aktívan az adatforgalmat, csak megfigyeli azt.
- Ez a támadás típus különösen veszélyes olyan hálózatokon, ahol nagy a forgalom, mivel a sok aktív munkamenet között a támadó könnyebben rejtőzködhet.
- A felhasználók különösen sebezhetőek erre a támadásra nem biztonságos vagy nyilvános Wi-Fi hálózatokon.

## Védekezési lehetőségek

A session sniffing elleni védekezés leghatékonyabb módjai:

- Titkosított kapcsolatok használata (HTTPS) minden oldalon, nem csak a bejelentkezésnél.
- Biztonságos hálózatok használata, különösen érzékeny műveletek végrehajtásakor.
- Munkamenet-tokenek rendszeres frissítése és érvénytelenítése.
- Anomália-detekció alkalmazása a felhasználói viselkedés és IP-címek monitorozásával.

A session sniffing elleni védelem kulcsfontosságú az online biztonság megőrzésében, különösen a mai, egyre inkább összekapcsolt digitális világban.

## Session sniffing eszközei

A session sniffing során a támadók különböző eszközöket használnak a hálózati forgalom megfigyelésére és a munkamenet-adatok elfogására. Íme néhány gyakran használt eszköz:

### Wireshark

Ez az egyik legismertebb és legszélesebb körben használt hálózati forgalomelemző eszköz. A Wireshark számos előnnyel rendelkezik:

- Széles protokoll-támogatás
- Könnyen használható grafikus felület
- Statisztikai elemzési lehetőségek
- Hálózati munkamenetek követése
- SSL/TLS forgalom dekódolása

URL: [wireshark.org](https://www.wireshark.org)

### Ettercap

Ez egy sokoldalú szoftvercsomag, amely lehetővé teszi a man-in-the-middle támadások végrehajtását. Főbb jellemzői:

- Hálózati szimatolás
- Protokoll-elemzés
- Tartalomszűrés
- Nyílt forráskódú és ingyenesen elérhető

URL: [ettercap-project.org](https://www.ettercap-project.org)

### CookieCatcher

Ez egy nyílt forráskódú eszköz, amely cross-site scripting (XSS) támadásokat használ a munkamenet-adatok megszerzésére. Jellemzői:

- Előre elkészített payloadok sütik ellopásához
- E-mail értesítések az újonnan megszerzett böngésző-sütikről

URL: [CookieCatcher GitHub](https://github.com/DisK0nn3cT/CookieCatcher)

### Burp Suite

Bár elsősorban nem sniffing eszköz, a Burp Proxy komponense hasznos lehet a forgalom elfogásához és módosításához.

URL: [portswigger.net/burp](https://portswigger.net/burp)