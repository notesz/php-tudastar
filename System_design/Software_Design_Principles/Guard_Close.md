# Guard Close

A guard clause-ok hatékony eszközök a PHP kódban a komplexitás csökkentésére és az olvashatóság javítására. Ez egy feltételes utasítás egy függvény vagy kódblokk elején, amely korán kilép, ha bizonyos feltétel teljesül. Célja, hogy megvédje a függvény fő logikáját a nemkívánatos feltételektől.

## Guard clause-ok előnyei

- **Jobb olvashatóság** \
Csökkenti a kód beágyazottságát és egyszerűbbé teszi a logika követését.

- **Korai kilépés** \
Lehetővé teszi a problémák korai szakaszban történő ellenőrzését.

- **Egyszerűbb hibakezelés** \
A kivételek kezelése a függvény elején történhet.

## Gyakorlati példák

### Hagyományos if-else helyett

```php
// Hagyományos megközelítés
function update($contact, $data) {
    if (valid($data)) {
        $contact->update($data);
    }
}

// Guard clause használatával
function update($contact, $data) {
    if (!valid($data)) {
        return;
    }
    $contact->update($data);
}
```

### Összetettebb példa

```php
// Guard clause-ok nélkül
function processOrder($order) {
    if ($order) {
        if ($order->items && count($order->items) > 0) {
            if ($order->paymentStatus === 'PAID') {
                // Fő logika a rendelés feldolgozásához
                echo 'Rendelés feldolgozása...';
            } else {
                echo 'Fizetés nem teljesült.';
            }
        } else {
            echo 'Nincsenek tételek a rendelésben.';
        }
    } else {
        echo 'Érvénytelen rendelés.';
    }
}

// Guard clause-okkal
function processOrder($order) {
    if (!$order) {
        echo 'Érvénytelen rendelés.';
        return;
    }
    
    if (!$order->items || count($order->items) === 0) {
        echo 'Nincsenek tételek a rendelésben.';
        return;
    }
    
    if ($order->paymentStatus !== 'PAID') {
        echo 'Fizetés nem teljesült.';
        return;
    }
    
    // Fő logika a rendelés feldolgozásához
    echo 'Rendelés feldolgozása...';
}
```