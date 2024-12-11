# API throttling és Rate Limiting

Az API throttling egy olyan technika, amely szabályozza az API-khoz érkező kérések számát és sebességét. A throttling fő célja az API-k teljesítményének és stabilitásának megőrzése, valamint a méltányos erőforrás-elosztás biztosítása a felhasználók között.

## A Throttling működése

- Ideiglenesen blokkolja azokat a klienseket, amelyek túllépik az engedélyezett kérési rátát.
- Korlátozza a kérések számát egy meghatározott időintervallumon belül.
- Különböző módszerekkel implementálható, például:
	- Kérések queue-ba állítása
	- Párhuzamos kérések korlátozása
	- Sávszélesség-korlátozás

## A Throttling előnyei

1. Teljesítmény és stabilitás: Megakadályozza a szerver túlterhelését és biztosítja a konzisztens válaszidőket.
2. Méltányos erőforrás-elosztás: Egyenlő hozzáférést biztosít minden felhasználó számára.
3. Skálázhatóság: Segít a kiszámítható terhelés kezelésében.
4. Biztonság: Védelmet nyújt a túlterheléses (DDoS) támadások ellen.
5. Felelősségteljes használat ösztönzése: A fejlesztőket hatékonyabb kódolásra ösztönzi.

## Rate Limiting

A Rate Limiting hasonló, mint a Throttling. Kevésbé agresszívebb módszer, mint a Throttling.

1. Inkább lelassítja a kéréseket, de nem állítja le teljesen.
2. Általában hosszabb időintervallumokra vonatkozik (pl. óra, nap, hónap).
3. Célja a hosszú távú erőforrás-használat szabályozása és a méltányos elosztás biztosítása.
4. Típusai:
	1. Felhasználói szintű korlátozás
	2. Földrajzi alapú korlátozás
	3. Szerver szintű korlátozás

## Rate Limiting a gyakorlatban

A következő PHP kód egy egyszerű rate limiting megoldást mutat be Redis használatával, amelyben IP címenként 5 kérést engedélyezünk 60 másodpercenként.

```php
<?php

// Redis kapcsolat létrehozása
$redis = new Redis();
$redis->connect('localhost', 6379);

// Rate limiting beállítások
$max_keresek = 5; // Maximális kérések száma
$idointervallum = 60; // Időintervallum másodpercekben

// Felhasználó IP címének lekérése
$ip_cim = $_SERVER['REMOTE_ADDR'];

// Redis kulcs létrehozása az IP cím alapján
$kulcs = "rate_limit:{$ip_cim}";

// Jelenlegi kérések számának lekérése
$keresek_szama = $redis->get($kulcs);

if ($keresek_szama === false) {
    // Ha még nincs kulcs, létrehozzuk és beállítjuk az értékét 1-re
    $redis->set($kulcs, 1);
    $redis->expire($kulcs, $idointervallum);
    $keresek_szama = 1;
} else {
    // Ha már létezik a kulcs, növeljük az értékét
    $keresek_szama = $redis->incr($kulcs);
}

if ($keresek_szama > $max_keresek) {
    // Ha túlléptük a limitet, hibaüzenetet küldünk
    http_response_code(429);
    exit;
}
```

Ez a kód a következőképpen működik:

1. Létrehozunk egy kapcsolatot a Redis szerverrel.
2. Beállítjuk a rate limiting paramétereit: maximális kérések száma és időintervallum.
3. Lekérjük a felhasználó IP címét.
4. Létrehozunk egy egyedi kulcsot a Redis-ben az IP cím alapján.
5. Ellenőrizzük, hogy létezik-e már ez a kulcs:
   - Ha nem, létrehozzuk és beállítjuk az értékét 1-re.
   - Ha igen, növeljük az értékét.
6. Ellenőrizzük, hogy a kérések száma meghaladja-e a limitet:
   - Ha igen, 429-es HTTP státuszkódot küldünk.