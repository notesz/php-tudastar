# Clean Code

A Clean Code, vagyis a tiszta kód egy olyan szoftverfejlesztési megközelítés, amely a könnyen olvasható, érthető és karbantartható kód írására összpontosít. A koncepciót Robert Cecil Martin (ismertebb nevén Uncle Bob) népszerűsítette "Clean Code: A Handbook of Agile Software Craftsmanship" című 2008-as könyvében.

## A Clean Code fő jellemzői

- **Olvashatóság**: A tiszta kód olyan, mint egy jól megírt próza - könnyen érthető és követhető.
- **Egyszerűség**: Közvetlen és lényegre törő, kerüli a felesleges bonyolultságot.
- **Karbantarthatóság**: Könnyen módosítható és továbbfejleszthető, akár nem az eredeti szerző által is.
- **Tesztelhetőség**: Rendelkezik egység- és elfogadási tesztekkel.

## Clean Code alapelvek

1. **Értelmes elnevezések**: A változók, függvények és osztályok neve legyen leíró és egyértelmű.

2. **Egy felelősség elve (SRP)**: Minden osztálynak és függvénynek csak egy feladata legyen.

3. **DRY (Don't Repeat Yourself)**: Kerüljük a kód ismétlődését, használjunk újrafelhasználható komponenseket.

4. **Függvények egyszerűsége**: A függvények legyenek rövidek, és csak egy dolgot csináljanak.

5. **Megfelelő kommentelés**: Csak akkor használjunk kommenteket, ha valóban szükséges további magyarázat.

6. **Kód formázása**: Használjunk következetes formázást és whitespace-t a kód vizuális tagolására.

7. **Hibakezelés**: Legyen átgondolt és teljes körű.

8. **Tesztek írása**: Alkalmazzunk unit teszteket és TDD (Test Driven Development) módszertant.

A Clean Code alkalmazása javítja a kód minőségét, csökkenti a hibák előfordulásának esélyét, és megkönnyíti a csapatmunkát. Bár időbe telhet elsajátítani ezeket az elveket, hosszú távon jelentősen növelik a fejlesztés hatékonyságát és a szoftver minőségét.

## Gyakorlati példák

### Értelmes elnevezések

- Használjunk leíró változó- és függvényneveket:

```php
// Rossz
$x = 5;

// Jó
$total_score = 5;
```

- Kerüljük a félrevezető neveket:

```php
// Rossz
$user_array = ['John', 'Jane', 'Bob'];

// Jó
$user_list = ['John', 'Jane', 'Bob'];
```

### Rövid és egyszerű függvények

- Egy függvény lehetőleg csak egy dolgot végezzen:

```php
// Rossz
function processOrder($order) {
    // Rendelés ellenőrzése
    // Fizetés feldolgozása
    // Email küldése
    // Raktárkészlet frissítése
}

// Jó
function processOrder($order) {
    validateOrder($order);
    processPayment($order);
    sendConfirmationEmail($order);
    updateInventory($order);
}
```

### Megfelelő kommentelés

- Kerüljük a felesleges kommenteket, helyette írjunk önmagát magyarázó kódot:

```php
// Rossz
// Ez a függvény kiszámolja az árengedményt
function calculateDiscount($price) {
    return $price * 0.1; // 10% kedvezmény
}

// Jó
const TEN_PERCENT_DISCOUNT = 0.1;

function calculateDiscount($price) {
    return $price * TEN_PERCENT_DISCOUNT;
}
```

### DRY elv alkalmazása

- Kerüljük a kód ismétlődését:

```php
// Rossz
function calculateBookPrice($quantity, $price) {
    return $quantity * $price;
}

function calculateLaptopPrice($quantity, $price) {
    return $quantity * $price;
}

// Jó
function calculateTotalPrice($quantity, $price) {
    return $quantity * $price;
}
```

### Formázás és szintaxis

- Használjunk konzisztens formázást és behúzást:

```php
// Rossz
if ($condition) {
doTask();
}elseif ($otherCondition){ doOtherTask();
}

// Jó
if ($condition) {
    doTask();
} elseif ($otherCondition) {
    doOtherTask();
}
```

### Mágikus számok elkerülése

- Használjunk konstansokat a kódban szereplő számértékek helyett:

```php
// Rossz
if ($age >= 65) {
    echo 'Kedvezmény';
}

// Jó
const NYUGDIJKORHATAR = 65;
if ($age >= NYUGDIJKORHATAR) {
    echo 'Kedvezmény';
}
```

### Típusozás használata

- Használjunk típusdeklarációkat a függvények paramétereinek és visszatérési értékeinek meghatározásához:

```php
// Jó
function addNumbers(int $a, int $b): int {
    return $a + $b;
}
```

### Kivételkezelés

- Használjunk megfelelő kivételkezelést a hibák kezelésére:

```php
// Jó
try {
    $result = divideNumbers($a, $b);
} catch (DivisionByZeroException $e) {
    logError($e->getMessage());
    displayUserFriendlyError('Nullával való osztás nem megengedett.');
}
```