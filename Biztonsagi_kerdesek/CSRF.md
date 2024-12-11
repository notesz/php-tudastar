# CSRF (Cross-Site Request Forgery)

A CSRF (Cross-Site Request Forgery), más néven keresztoldali kéréshamisítás egy olyan támadási módszer, amely során a támadó arra kényszeríti az áldozatot, hogy nem kívánt műveleteket hajtson végre egy olyan webalkalmazásban, amelybe már be van jelentkezve.

## Működési elv

- A támadó kihasználja a webalkalmazás bizalmát a hitelesített felhasználóval szemben.
- A támadás során az áldozat böngészője automatikusan elküldi a hitelesítési adatokat (pl. munkamenet-sütit) a célzott weboldalnak.
- A webalkalmazás nem tudja megkülönböztetni a valódi és a hamisított kéréseket.

## Támadás menete

1. A támadó azonosít egy olyan kérést, amely valamilyen állapotváltozást idéz elő (pl. jelszóváltoztatás).
2. Létrehoz egy olyan weboldalt vagy e-mailt, amely tartalmazza ezt a kérést.
3. Az áldozatot ráveszi, hogy látogassa meg ezt az oldalt vagy nyissa meg az e-mailt.
4. A kérés az áldozat nevében, annak tudta nélkül kerül végrehajtásra.
## Védekezési módszerek

A CSRF (Cross-Site Request Forgery) támadások megelőzésére több hatékony módszer is létezik. Íme néhány kulcsfontosságú technika:

### CSRF-tokenek használata

A CSRF-tokenek alkalmazása az egyik leghatékonyabb védekezési módszer:

- Minden állapotváltoztató kéréshez egyedi, titkos és kiszámíthatatlan tokent kell generálni.
- A tokent a szerver hozza létre és tárolja.
- A token bekerül a formokba rejtett mezőként.
- A szerver ellenőrzi a beérkező kérésekben szereplő tokent.

### SameSite sütik alkalmazása

A SameSite süti attribútum beállítása segít megelőzni a CSRF támadásokat:

- Strict: A süti csak ugyanarról a domainről érkező kérésekhez kerül elküldésre.
- Lax: Engedélyezi a süti küldését top-level navigációknál.
- None: Nem ajánlott, mert nem nyújt védelmet.

### Egyéb védekezési technikák

- Egyedi HTTP fejlécek használata AJAX/API hívásoknál.
- Erősebb hitelesítés megkövetelése érzékeny műveleteknél (pl. jelszó újbóli megadása).
- REST alapelvek követése, GET kérések csak lekérdezésre használata.
- Beépített CSRF védelem használata a fejlesztői keretrendszerekben.

A CSRF elleni védelem kulcsfontosságú a webalkalmazások biztonságának megőrzésében. A fenti technikák kombinálásával jelentősen csökkenthető a CSRF támadások kockázata.