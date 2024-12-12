# OAuth

Az OAuth (Open Authorization) egy nyílt szabványú engedélyezési protokoll, amely lehetővé teszi a felhasználók számára, hogy biztonságosan hozzáférést adjanak alkalmazásoknak anélkül, hogy megosztanák jelszavaikat. Főbb jellemzői:

## Működése

- Tokeneket használ jelszavak helyett a hozzáférés biztosítására
- Lehetővé teszi harmadik fél alkalmazások számára korlátozott hozzáférést erőforrásokhoz
- Elkülöníti az autentikációt és az engedélyezést

## Főbb komponensei

- Erőforrás tulajdonos: a felhasználó, aki hozzáférést ad
- Kliens: az alkalmazás, amely hozzáférést kér
- Erőforrás szerver: ahol a védett erőforrások találhatók
- Engedélyezési szerver: hitelesíti a felhasználót és tokeneket bocsát ki

## Előnyei

- Növeli a biztonságot azáltal, hogy nem kell megosztani jelszavakat
- Részletes hozzáférés-szabályozást tesz lehetővé
- Széles körben elterjedt és támogatott

## Használata

- Webes és mobil alkalmazásoknál gyakori ("Bejelentkezés Facebook-kal" típusú funkciók)
- API-k védelmére használják
- Egyszeri bejelentkezés (SSO) megoldásokban alkalmazzák

## Hogyan működik az OAuth a gyakorlatban

Az OAuth egy engedélyezési protokoll, amely lehetővé teszi, hogy egy alkalmazás hozzáférjen egy felhasználó erőforrásaihoz anélkül, hogy megkapná a felhasználó jelszavát. A gyakorlatban az OAuth a következőképpen működik:

### Az OAuth folyamat főbb lépései

1. A felhasználó jelzi szándékát, hogy hozzáférést szeretne adni egy alkalmazásnak (kliensnek) valamely szolgáltatáshoz.

2. A kliens kér egy kérési tokent az engedélyezési szervertől.

3. A felhasználót átirányítják az engedélyezési szerverhez hitelesítésre.

4. A felhasználó jóváhagyja a hozzáférést.

5. A kliens megkapja az engedélyezési kódot.

6. A kliens ezt az engedélyezési kódot hozzáférési tokenre cseréli.

7. A kliens használhatja a hozzáférési tokent az erőforrások eléréséhez.

### Gyakorlati példák

#### Közösségi média bejelentkezés

Amikor egy weboldal lehetővé teszi a Facebook-fiókkal való bejelentkezést, az OAuth-t használja. A folyamat:

- A felhasználó a "Bejelentkezés Facebook-kal" gombra kattint.
- Az oldal átirányítja a Facebookra.
- A felhasználó jóváhagyja a hozzáférést.
- A Facebook visszairányítja a felhasználót az eredeti oldalra egy tokennel.
- Az oldal ezt a tokent használja a felhasználó adatainak lekéréséhez.

#### API hozzáférés

Például egy időjárás alkalmazás OAuth-t használhat a Google Naptár API-hoz való hozzáféréshez:

- Az alkalmazás kéri a felhasználó engedélyét.
- A felhasználó jóváhagyja a hozzáférést a Google-fiókjához.
- Az alkalmazás megkapja a hozzáférési tokent.
- Az alkalmazás ezt a tokent használja a naptáradatok lekéréséhez és események létrehozásához.

## OAuth 2.0 implementálása egy gyakorlati példában PHP-ban

Ez a példa bemutatja az OAuth 2.0 folyamat alapvető lépéseit:

1.	A felhasználó átirányítása az engedélyezési URL-re
2.	A visszahívás kezelése és a hozzáférési token beszerzése
3.	A felhasználói adatok lekérése a hozzáférési tokennel

Először telepítjük a `leauge/oauth2-client` csomagot:

```bash
composer require league/oauth2-client
```

Hozzunk létre egy `oauth.php` fájlt a következő tartalommal:

```php
<?php

require 'vendor/autoload.php';

use League\OAuth2\Client\Provider\GenericProvider;

$provider = new GenericProvider([
    'clientId'     => 'AZ_ÖN_KLIENS_ID-JA',
    'clientSecret' => 'AZ_ÖN_KLIENS_TITKA',
    'redirectUri'  => 'http://example.com/callback.php',
    'urlAuthorize' => 'https://szolgaltato.com/oauth2/authorize',
    'urlAccessToken' => 'https://szolgaltato.com/oauth2/token',
    'urlResourceOwnerDetails' => 'https://szolgaltato.com/api/user'
]);

// Kezdeményezzük az OAuth folyamatot
if (!isset($_GET['code'])) {
    $authorizationUrl = $provider->getAuthorizationUrl();
    $_SESSION['oauth2state'] = $provider->getState();
    header('Location: ' . $authorizationUrl);
    exit;
}

// Kezeljük a visszahívást
if (isset($_GET['code'])) {
    try {
        $accessToken = $provider->getAccessToken('authorization_code', [
            'code' => $_GET['code']
        ]);

        $resourceOwner = $provider->getResourceOwnerDetails($accessToken);
        
        // Használjuk a felhasználói adatokat
        var_export($resourceOwner->toArray());

    } catch (\League\OAuth2\Client\Provider\Exception\IdentityProviderException $e) {
        exit($e->getMessage());
    }
}
```

## A League OAuth 2.0 szerver telepítése

A League OAuth2-server könyvtár telepítéséhez [teljes leírás itt található](https://oauth2.thephpleague.com/installation/).
