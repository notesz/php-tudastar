# GraphQL

A GraphQL egy adatlekérdezési nyelv API-khoz, amelyet a Facebook fejlesztett ki. A GraphQL lehetővé teszi a kliensek számára, hogy pontosan meghatározzák, milyen adatokra van szükségük ("deklaratív adatlekérdezés").

## Főbb jellemzők

- **XML-alapú**:
  A GraphQL üzenetek XML formátumúak, ami biztosítja a platformfüggetlenséget.
- **Típusos rendszer**:
  Erősen típusos, ami segít a konzisztencia és a típusbiztonság fenntartásában.
- **Egyetlen végpont**:
  A GraphQL API-k általában egyetlen végpontot használnak.
- **Rugalmas lekérdezések**:
  A kliensek pontosan meghatározhatják, milyen adatokat szeretnének lekérni.
## Működése

A GraphQL három fő műveletet támogat:

1. **Lekérdezések**:
   Adatok olvasására szolgálnak.
2. **Mutációk**:
   Adatok létrehozására, frissítésére vagy törlésére használatosak.
3. **Feliratkozások**:
   Valós idejű adatfrissítések fogadására alkalmasak.
## Előnyök

- **Hatékony adatlekérdezés**:
  Csökkenti a túl- és alullekérdezést.
- **Egyetlen kérés, több erőforrás**:
  Lehetővé teszi több adat lekérését egyetlen API-híváson keresztül.
- **Rugalmas séma**:
  Könnyebb API-evolúció verziószámozás nélkül.
- **Erős típusosság**:
  Javítja a fejlesztési folyamat konzisztenciáját és biztonságát.
- **Automatikus dokumentáció**:
  A séma önmagát dokumentálja.
## Hátrányok

- **Komplexitás**:
  Összetett lekérdezések esetén teljesítményproblémák léphetnek fel.
- **Tanulási görbe**:
  A fejlesztőknek meg kell tanulniuk a GraphQL sémadefiníciós nyelvet.
- **Gyorsítótárazási kihívások**:
  Nem támaszkodik a hagyományos HTTP-gyorsítótárazási módszerekre.
## GraphQL hívás a gyakorlatban

Az alábbi példában egy GraphQL hívás történik PHP-ban (Guzzle kliens használatával):

```php
<?php

require 'vendor/autoload.php';

use GuzzleHttp\Client;

$client = new Client();

$query = <<<'GRAPHQL'
query {
  user(id: "123") {
    id
    name
    email
    posts {
      id
      title
    }
  }
}
GRAPHQL;

try {
    $response = $client->request('POST', 'https://api.peldagraphql.hu/graphql', [
        'json' => [
            'query' => $query
        ],
        'headers' => [
            'Content-Type' => 'application/json',
            'Authorization' => 'Bearer YOUR_ACCESS_TOKEN'
        ]
    ]);

    $data = json_decode($response->getBody(), true);

    if (isset($data['data'])) {
        $user = $data['data']['user'];
        echo "Felhasználó neve: " . $user['name'] . "\n";
        echo "E-mail címe: " . $user['email'] . "\n";
        echo "Bejegyzések:\n";
        foreach ($user['posts'] as $post) {
            echo "- " . $post['title'] . "\n";
        }
    } else {
        echo "Hiba történt a lekérdezés során.\n";
    }

} catch (\Exception $e) {
    echo "Hiba: " . $e->getMessage();
}
```

Ebben a példában:

1. Először betöltjük a Composer autoloadert (feltételezve, hogy a Guzzle telepítve van).
2. Létrehozunk egy Guzzle kliens példányt.
3. Definiáljuk a GraphQL lekérdezést egy heredoc szintaxissal.
4. A `try-catch` blokkon belül küldünk egy POST kérést a GraphQL végponthoz.
5. A kérés törzsében JSON formátumban küldjük el a lekérdezést.
6. A fejlécekben beállítjuk a Content-Type-ot és egy példa Bearer tokent a hitelesítéshez.
7. A válasz feldolgozása során kiírjuk a lekért felhasználói adatokat és a bejegyzések címeit.
8. Hiba esetén kiírjuk a hibaüzenetet.