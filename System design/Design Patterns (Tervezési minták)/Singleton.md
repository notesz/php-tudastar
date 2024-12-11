# Singleton

A **Singleton** design pattern egy **Creational Pattern** (létrehozási minta), amely biztosítja, hogy egy osztályból csak egyetlen példány létezhessen a program futása során, és globális hozzáférést biztosít ehhez az egy példányhoz. Ez a minta gyakran használatos olyan helyzetekben, amikor egy központi vezérlő vagy erőforráskezelő objektumra van szükség.

## Működése

1. **Privát konstruktor**:

   - Az osztály konstruktora privát, hogy megakadályozza az új példányok létrehozását kívülről.

2. **Statikus példány tárolása**:

   - Az osztály rendelkezik egy privát statikus tulajdonsággal, amely tárolja az osztály egyetlen példányát.

3. **Statikus hozzáférési metódus**:

   - Egy nyilvános statikus metódus biztosítja a hozzáférést az osztály példányához. Ha a példány még nem létezik, akkor létrehozza azt, különben visszaadja a már meglévőt.

### Példa PHP-ban

Íme egy egyszerű Singleton minta implementáció PHP-ban:

```php
class Singleton {
    // A statikus tulajdonság az osztály egyetlen példányát tárolja
    private static $instance = null;

    // Privát konstruktor megakadályozza az új példányok létrehozását
    private function __construct() {
        echo "Singleton példány létrejött.\n";
    }

    // Megakadályozzuk a klónozást
    private function __clone() {}

    // Megakadályozzuk a sorosítást (serialize)
    private function __wakeup() {}

    // Statikus metódus az egyetlen példány eléréséhez
    public static function getInstance() {
        if (self::$instance === null) {
            self::$instance = new Singleton();
        }
        return self::$instance;
    }

    // Példaként egy metódus
    public function doSomething() {
        echo "Singleton működik.\n";
    }
}

// Használat
$singleton1 = Singleton::getInstance();
$singleton1->doSomething();

$singleton2 = Singleton::getInstance();
$singleton2->doSomething();

// Ellenőrzés: ugyanaz az objektum mindkét esetben
var_dump($singleton1 === $singleton2); // true
```

## Fontos jellemzők

1. **Egyetlen példány**:

   - A `Singleton::getInstance()` mindig ugyanazt az objektumpéldányt adja vissza.

2. **Globális hozzáférés**:

   - Az osztály mindenhol elérhető a statikus metóduson keresztül.

3. **Privát konstruktor**:

   - Megakadályozza az új példányok létrehozását kívülről.

4. **Statikus tárolás**:

   - Az osztály példánya statikusan van tárolva, így minden hívás ugyanazt az objektumot használja.

## Mikor használd?

A Singleton pattern akkor hasznos, ha:

- Egy központi vezérlő objektumra van szükség (pl. konfigurációkezelő, naplózó).
- Egy erőforrás megosztott használatára van szükség (pl. adatbáziskapcsolat).

## Előnyök

- Biztosítja, hogy csak egyetlen példány létezzen.
- Könnyen elérhető globális hozzáférési pontot biztosít.
- Csökkenti a memóriahasználatot megosztott erőforrások esetén.

## Hátrányok

- A globális állapot bevezetése miatt nehezebb lehet tesztelni (pl. egységtesztek).
- Ha túlzottan használják, csökkentheti a kód modularitását és bővíthetőségét.
- Többszálú környezetben megfelelő szinkronizáció nélkül problémák léphetnek fel (pl. versenyhelyzetek).

A Singleton design pattern hatékony megoldás lehet bizonyos helyzetekben, de érdemes körültekintően alkalmazni, hogy elkerüljük a túlzott függőségeket és a kód olvashatóságának romlását.