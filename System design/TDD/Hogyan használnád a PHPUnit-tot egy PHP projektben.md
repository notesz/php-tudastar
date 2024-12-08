A PHPUnit használata egy PHP projektben viszonylag egyszerű folyamat. Íme egy lépésenkénti útmutató egy egyszerű egységteszt példával:

1. Először telepítsd a PHPUnit-ot a projektedben Composer segítségével:

```bash
composer require --dev phpunit/phpunit
```

2. Hozz létre egy `tests` mappát a projekt gyökérkönyvtárában a tesztek tárolására.

3. Írd meg a tesztelendő kódot. Például legyen egy egyszerű `Calculator` osztályunk:

```php
<?php

class Calculator {
    public function add($a, $b) {
        return $a + $b;
    }
}
```

4. Hozz létre egy tesztfájlt a `tests` mappában, például `CalculatorTest.php` néven:

```php
<?php

use PHPUnit\Framework\TestCase;

class CalculatorTest extends TestCase {
    public function testAdd() {
        $calculator = new Calculator();
        $result = $calculator->add(2, 3);
        $this->assertEquals(5, $result);
    }
}
```

Ebben a példában:

- A tesztosztály kiterjeszti a `PHPUnit\Framework\TestCase` osztályt.
- A tesztmetódus neve `test`-tel kezdődik.
- Az `assertEquals` metódust használjuk az elvárt és a tényleges eredmény összehasonlítására.

5. A teszt futtatásához használd a következő parancsot a terminálban:

```bash
./vendor/bin/phpunit --verbose tests
```

Ez a parancs lefuttatja az összes tesztet a `tests` mappában.

A PHPUnit számos hasznos funkciót kínál, mint például adatszolgáltatók használata, kivételek tesztelése, vagy mock objektumok létrehozása. Ezekkel a funkciókkal komplex teszteket is könnyen megírhatsz és futtathatsz a PHP projektedben.