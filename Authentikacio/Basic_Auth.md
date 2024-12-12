# Basic Auth

A Basic Authentication (Basic Auth) egy egyszerű hitelesítési módszer, amelyet HTTP protokollban használnak.

## Működése

- A felhasználó egy felhasználónevet és jelszót ad meg a kérés során.
- Ezeket az adatokat base64 kódolással titkosítják és az Authorization HTTP fejlécben küldik el.
- A fejléc formátuma: "Authorization: Basic <kódolt_adatok>"

## Előnyei

- Egyszerű implementálni és használni
- Beépített a HTTP protokollba
- Nem igényel cookie-kat vagy munkamenet-azonosítókat

## Hátrányai

- Nem biztonságos titkosítás nélkül (pl. HTTPS)
- A jelszó minden kérésnél elküldésre kerül
- Nincs beépített kijelentkezési mechanizmus
- Korlátozott felhasználói élmény

## Használata

Főleg egyszerűbb alkalmazásoknál vagy API-knál alkalmazzák, ahol nincs szükség összetettebb hitelesítésre. Biztonsági okokból mindig HTTPS-sel együtt ajánlott használni.

## A Basic Auth használata a gyakorlatban

### Szerver oldali implementáció NGINX oldalon

A Basic Authentication beállítása NGINX-ben a következő lépésekkel történik:

#### 1. Jelszófájl létrehozása

Először létre kell hozni egy jelszófájlt a felhasználónevekkel és jelszavakkal. Ezt az `htpasswd` segédprogrammal tehetjük meg:

```bash
sudo htpasswd -c /etc/nginx/.htpasswd felhasznalonev
```

#### 2. NGINX konfigurálása

Ezután módosítjuk a konfigurációs fájlt:

```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        auth_basic "Védett terület";
        auth_basic_user_file /etc/nginx/.htpasswd;
        # További konfigurációs beállítások...
    }
}
```

#### 3. NGINX újraindítása

Végül újra kell indítani az NGINX-et:

```bash
sudo systemctl reload nginx
```

### Szerver oldali implementáció PHP-ban

Az alábbi kóddal ellenőrizhetük, hogy a kliens küldött-e hitelesítési adatokat:

```php
<?php

if (!isset($_SERVER['PHP_AUTH_USER'])) {
    header('WWW-Authenticate: Basic realm="Az én területem"');
    header('HTTP/1.0 401 Unauthorized');
    echo 'Hozzáférés megtagadva';
    exit;
}
```

### Kliens oldali használat PHP-ban

PHP cURL használatával a következőképpen küldhetünk Basic Auth hitelesítést tartalmazó kérést:

```php
<?php

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'http://peldaapi.hu/endpoint');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
curl_setopt($ch, CURLOPT_USERPWD, "felhasznalonev:jelszo");

$response = curl_exec($ch);
curl_close($ch);
```