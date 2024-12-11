# REST API

A REST API (Representational State Transfer Application Programming Interface) egy olyan interfész, amely lehetővé teszi különböző webes alkalmazások és szolgáltatások közötti kommunikációt.

## REST API működése

A REST API a HTTP protokollt használja az adatátvitelre, és **általában JSON formátumban kommunikál**. A működése a következő lépésekből áll:

1. A kliens kérést küld a szervernek egy egyedi erőforrás-azonosító (URL) segítségével.
2. A szerver hitelesíti a klienst és ellenőrzi a jogosultságokat.
3. A szerver feldolgozza a kérést.
4. A szerver választ küld a kliensnek, amely tartalmazza a kért információkat vagy a művelet eredményét.

## Főbb jellemzők

### Erőforrás-orientált

A REST API-k erőforrások köré szerveződnek. Az erőforrások lehetnek adatok, objektumok vagy szolgáltatások, amelyeket egyedi azonosítókkal (URI-kkal) lehet elérni.

### HTTP metódusok

A REST API a standard HTTP metódusokat használja az erőforrásokon végzett műveletek végrehajtásához:

- GET: erőforrás lekérése
- POST: új erőforrás létrehozása
- PUT: meglévő erőforrás frissítése vagy létrehozása
- PATCH: erőforrás részleges frissítése
- DELETE: erőforrás törlése

### Egységes interfész

A REST API-k egységes interfészt használnak, amely segít az ügyfél és a szolgáltatás implementálásának különválasztásában.

## Példa működésre

Képzeljünk el egy egyszerű blog REST API-t:

```
POST https://api.example.com/posts
Content-Type: application/json

{
"title": "REST API",
"text": "A REST API (Representational State Transfer Application Programming Interface) egy olyan interfész, amely lehetővé teszi különböző webes alkalmazások és szolgáltatások közötti kommunikációt.",
"tags": ["API", "REST", "PHP"]
}
```

## Gyakori hitelesítési módszerek a REST API hívásra

### Alapszintű hitelesítés (Basic Authentication)

Ez a legegyszerűbb módszer, ahol a felhasználónevet és jelszót közvetlenül küldik el a kérés fejlécében. Például:

```php
<?php

$url = "https://api.example.com";
$felhasznalonev = "felhasznalo";
$jelszo = "jelszo";

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
curl_setopt($ch, CURLOPT_USERPWD, $felhasznalonev . ":" . $jelszo);

$valasz = curl_exec($ch);
$http_kod = curl_getinfo($ch, CURLINFO_HTTP_CODE);

curl_close($ch);

echo "HTTP válaszkód: " . $http_kod;
```

### Token alapú hitelesítés

Ebben az esetben a szerver egy egyedi tokent generál a sikeres bejelentkezés után, amit a kliens minden további kérésnél használ. Például:

```php
<?php

$url = "https://api.example.com";
$token = "egyedi_token_123456";

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
    "Authorization: Bearer " . $token
));

$valasz = curl_exec($ch);
$http_kod = curl_getinfo($ch, CURLINFO_HTTP_CODE);

curl_close($ch);
```

### API kulcs hitelesítés

Az API szolgáltató egy egyedi kulcsot ad minden kliensnek, amit a kérésekben kell használni. Például:

```php
<?php

$url = "https://api.example.com";
$api_kulcs = "titkos_api_kulcs_123";

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
    "Authorization: api-key " . $api_kulcs
));

$valasz = curl_exec($ch);
$http_kod = curl_getinfo($ch, CURLINFO_HTTP_CODE);

curl_close($ch);

echo "HTTP válaszkód: " . $http_kod;
```

### OAuth 2.0

Ez egy összetettebb protokoll, amely lehetővé teszi a felhasználók számára, hogy hozzáférést adjanak az adataikhoz anélkül, hogy megosztanák a jelszavukat. Különösen hasznos, amikor külső szolgáltatásokhoz (pl. Google, Facebook) kell hozzáférni.

## Biztonsági megfontolások

- Mindig használjon HTTPS-t a kommunikáció titkosításához.
- Kerülje az alapszintű hitelesítést érzékeny adatok esetén vagy éles környezetben.
- A tokeneket célszerű titkosítani (pl. JWT vagy OAuth segítségével) és rövid élettartamúra állítani.
- Implementáljon hozzáférés-vezérlési listákat (ACL) a jogosultságok finomhangolásához.