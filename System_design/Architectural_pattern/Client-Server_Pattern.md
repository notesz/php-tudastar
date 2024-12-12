# Client-Server Pattern

A Client-Server Pattern két fő komponensre osztja fel a rendszert: kliensekre és szerverekre. Ez a minta a feladatok és erőforrások megosztását teszi lehetővé a szolgáltatást nyújtók (szerverek) és a szolgáltatást igénylők (kliensek) között.

## Fő jellemzők

- **Centralizált struktúra**: A szerver központi erőforrásként működik, amelyhez a kliensek kapcsolódnak.
- **Elkülönített felelősségek**: A kliensek általában a felhasználói felületet és az interakciót kezelik, míg a szerverek az adatfeldolgozást és -tárolást végzik.
- **Kétirányú kommunikáció**: A kliensek kéréseket küldenek a szervernek, a szerver pedig válaszol ezekre.

## Működési elv

1. A kliens kérést küld a szervernek.
2. A szerver fogadja és feldolgozza a kérést.
3. A szerver visszaküldi a választ a kliensnek.
4. A kapcsolat általában lezárul a válasz után.

## Előnyök

- **Központosított adatkezelés**: Könnyebb adatmenedzsment és frissítés.
- **Skálázhatóság**: A kliensek és szerverek száma külön-külön növelhető.
- **Biztonság**: Az adatok központilag védhetők és kezelhetők.

## Hátrányok

- **Túlterhelés lehetősége**: Ha túl sok kliens kér adatot egyszerre, a szerver túlterhelődhet.
- **Egypontos meghibásodás**: Ha a szerver leáll, az egész rendszer működésképtelenné válhat.

## Gyakorlati példa a Client-Server Pattern-ra

Ez egy egyszerűsített példa, ami jól szemlélteti a minta lényegét. \
A példában
- a szerver folyamatosan fut és várja a kliensek kapcsolódását,
- a kliens kapcsolódik a szerverhez (kérést küld, majd fogadja a választ) és
- a szerver fogadja a kliens kérését, feldolgozza azt és visszaküldi a választ.

### Szerver oldal (server.php)

Először nézzük meg a szerver oldali kódot:

```php
<?php

// Szerver beállítása
$host = '127.0.0.1';
$port = 8080;

// Socket létrehozása
$socket = socket_create(AF_INET, SOCK_STREAM, SOL_TCP);
socket_bind($socket, $host, $port);
socket_listen($socket);

echo "Szerver fut a $host:$port címen...\n";

while (true) {
    // Kliens kapcsolat elfogadása
    $client = socket_accept($socket);
    
    // Kérés fogadása
    $request = socket_read($client, 1024);
    echo "Kérés érkezett: $request\n";
    
    // Válasz küldése
    $response = "Szerver válasza: " . date("Y-m-d H:i:s");
    socket_write($client, $response, strlen($response));
    
    // Kapcsolat lezárása
    socket_close($client);
}

socket_close($socket);
```

### Kliens oldal (client.php)

Most nézzük meg a kliens oldali kódot:

```php
<?php

// Kapcsolódási adatok
$host = '127.0.0.1';
$port = 8080;

// Socket létrehozása és kapcsolódás
$socket = socket_create(AF_INET, SOCK_STREAM, SOL_TCP);
$result = socket_connect($socket, $host, $port);

if ($result === false) {
    echo "Kapcsolódási hiba: " . socket_strerror(socket_last_error()) . "\n";
} else {
    echo "Kapcsolódva a szerverhez.\n";
    
    // Kérés küldése
    $request = "Idő lekérdezése";
    socket_write($socket, $request, strlen($request));
    
    // Válasz fogadása
    $response = socket_read($socket, 1024);
    echo "Szerver válasza: $response\n";
}

socket_close($socket);
```

### Használat

1. Indítsd el a szervert egy terminálban:
   ```
   php server.php
   ```

2. Futtasd a klienst egy másik terminálban:
   ```
   php client.php
   ```
