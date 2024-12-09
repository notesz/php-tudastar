A JWT (JSON Web Token) egy nyílt szabvány, amely biztonságos információmegosztást tesz lehetővé általában egy kliens és egy szerver között.
## A JWT működése

A JWT (JSON Web Token) alapú hitelesítés a következőképpen működik:
### Bejelentkezés folyamata

1. A felhasználó megadja a hitelesítő adatait (pl. felhasználónév és jelszó).
2. A szerver ellenőrzi ezeket az adatokat.
3. Ha érvényesek, a szerver létrehoz egy JWT-t, amely tartalmazza a felhasználó azonosítóját és esetleg más releváns információkat.
4. A szerver digitálisan aláírja a tokent egy titkos kulccsal.
5. A szerver visszaküldi a JWT-t a kliensnek.
### Token használata

1. A kliens eltárolja a JWT-t (általában localStorage-ban vagy cookie-ban).
2. Minden további kérésnél a kliens elküldi a JWT-t a szervernek (általában az Authorization fejlécben).
3. A szerver ellenőrzi a token aláírását és érvényességét.
4. Ha érvényes, a szerver feldolgozza a kérést és visszaküldi a választ.
### Előnyök

- Állapotmentesség: A szerver nem tárol munkamenet-információkat.
- Skálázhatóság: Könnyen használható elosztott rendszerekben.
- Hatékonyság: Csökkenti az adatbázis-lekérdezések számát.
### Biztonsági megfontolások

- A JWT-ket biztonságosan kell tárolni a kliens oldalon.
- Érdemes rövid lejárati időt beállítani a tokeneknek.
- Használjunk HTTPS-t a kommunikáció titkosításához.

## Gyakorlati példa a JWT működésére

A példában JWT használata PHP-ban történik, a `firebase/php-jwt` csomag használatával.

```php
<?php

require 'vendor/autoload.php';
use Firebase\JWT\JWT;
use Firebase\JWT\Key;

// Titkos kulcs a token aláírásához
$key = "az_ön_titkos_kulcsa";

// Token létrehozása
function createToken($userId) {
    global $key;
    $payload = [
        "iss" => "http://example.org",
        "aud" => "http://example.com",
        "iat" => time(),
        "exp" => time() + 3600,
        "userId" => $userId
    ];

    $jwt = JWT::encode($payload, $key, 'HS256');
    return $jwt;
}

// Token ellenőrzése
function verifyToken($token) {
    global $key;
    try {
        $decoded = JWT::decode($token, new Key($key, 'HS256'));
        return $decoded;
    } catch (Exception $e) {
        return false;
    }
}

// Példa használat
$userId = 123;
$token = createToken($userId);
echo "Létrehozott token: " . $token . "\n";

$decoded = verifyToken($token);
if ($decoded) {
    echo "Token érvényes. Felhasználó ID: " . $decoded->userId . "\n";
} else {
    echo "Érvénytelen token.\n";
}
```

Ez a példa bemutatja:

1. Token létrehozását a `createToken` függvénnyel.
2. Token ellenőrzését a `verifyToken` függvénnyel.
3. A létrehozott token kiíratását.
4. A token ellenőrzését és a benne tárolt adatok kinyerését.

Fontos, hogy éles környezetben további biztonsági intézkedéseket kell alkalmazni. Például a token lejárati idejének és a kibocsátó ellenőrzését.