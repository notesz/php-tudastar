# CORS

A Cross-Origin Resource Sharing (CORS) egy olyan mechanizmus, amely lehetővé teszi a webböngészők számára, hogy biztonságosan megkerüljék az azonos eredetű (same-origin) szabályt, és hozzáférjenek más domainek erőforrásaihoz.

A CORS lényegében egy kontrollált módja annak, hogy egy weboldal más domainek erőforrásait használhassa.

## Működése

A CORS a következőképpen működik:

1. A böngésző HTTP kérést küld egy másik domainre, beleértve az Origin fejlécet, amely tartalmazza a kérést indító oldal eredetét.

2. A szerver válaszában CORS-specifikus fejléceket küld vissza, például:
   - `Access-Control-Allow-Origin`: meghatározza, mely eredeteknek engedélyezett a hozzáférés
   - `Access-Control-Allow-Methods`: engedélyezett HTTP metódusok
   - `Access-Control-Allow-Headers`: engedélyezett kérés fejlécek

3. A böngésző ellenőrzi ezeket a fejléceket és ha megfelelőek, engedélyezi az erőforrás elérését.

## Előnyök és használat

A CORS előnye például, hogy biztonságot nyújt az API-k és más webes szolgáltatások elérésére különböző helyekről. Gyakran használják külső API-k elérése kliensoldali JavaScript kódból.

## Példa CORS beállítására

A CORS (Cross-Origin Resource Sharing) konfigurációjában több módon lehet megadni a megengedett eredeti forrásokat:

### Specifikus források engedélyezése

A `Access-Control-Allow-Origin` fejléc használatával konkrét forrásokat engedélyezhetünk:

```
Access-Control-Allow-Origin: https://example.com
```

Ez csak az `https://example.com` domainről érkező kéréseket engedi.

### Több forrás engedélyezése

Több forrást is megadhatunk, például:

```
Access-Control-Allow-Origin: https://example.com
Access-Control-Allow-Origin: https://another-example.com
```

### Minden forrás engedélyezése

Ha minden forrásból érkező kérést engedélyezni szeretnénk:

```
Access-Control-Allow-Origin: *
```

Ez azonban biztonsági kockázatot jelenthet, ezért óvatosan használjuk.

### Wildcard használata

Lehetőség van wildcard karakterek használatára is, például:

```
Access-Control-Allow-Origin: https://*.example.com
```

Ez engedélyezi az összes `example.com` aldomainről érkező kérést.

### Dinamikus konfigurálás

Szerveroldali kódban dinamikusan is beállíthatjuk a megengedett forrásokat. Például:

```php
<?php

// Engedélyezett források listája
$allowed_origins = [
    'http://example.com',
    'https://example.com',
    'http://subdomain.example.com'
];

// A kérés eredetének ellenőrzése
$origin = $_SERVER['HTTP_ORIGIN'] ?? '';

if (in_array($origin, $allowed_origins)) {
    header("Access-Control-Allow-Origin: $origin");
    header("Access-Control-Allow-Methods: GET, POST, OPTIONS");
    header("Access-Control-Allow-Headers: Content-Type, Authorization");
    header("Access-Control-Allow-Credentials: true");
}

// Ha preflight OPTIONS kérés érkezik
if ($_SERVER['REQUEST_METHOD'] == 'OPTIONS') {
    exit(0);
}

// A tényleges API logika itt következne
// ...
```

Fontos megjegyezni, hogy biztonsági okokból mindig csak a szükséges forrásokat engedélyezzük, és kerüljük a túl megengedő beállításokat.