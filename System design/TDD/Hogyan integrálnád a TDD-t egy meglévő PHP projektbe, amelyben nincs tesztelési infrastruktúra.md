Egy tesztelési infrastruktúra létrehozása egy meglévő PHP projekthez több lépésből áll, amelyeket fokozatosan lehet végrehajtani. Az alábbiakban bemutatom a szükséges lépéseket:

---

## **1. Tesztelési keretrendszer kiválasztása és telepítése**

A legnépszerűbb PHP tesztelési keretrendszer a PHPUnit, de más eszközök is elérhetők, mint például a Pest vagy a Codeception.

- Telepítsd a PHPUnit-t Composer segítségével:

```bash
composer require --dev phpunit/phpunit
```

- Hozz létre egy `phpunit.xml` konfigurációs fájlt a projekt gyökerében, amely tartalmazza az alapvető beállításokat:

```xml
<phpunit bootstrap="vendor/autoload.php">
    <testsuites>
        <testsuite name="Application Test Suite">
            <directory>tests</directory>
        </testsuite>
    </testsuites>
</phpunit>
```

---

## **2. Tesztmappa létrehozása**

- Hozz létre egy `tests` könyvtárat a projekt gyökerében a tesztek tárolására.
- Struktúráld a tesztmappát úgy, hogy tükrözze a projekt szerkezetét (pl. `tests/Controllers`, `tests/Models`).

---

## **3. Alapvető tesztesetek írása**

- Kezdj egyszerű egységtesztekkel (unit tests), amelyek egy-egy osztály vagy metódus működését ellenőrzik.
- Példa egy egyszerű egységtesztre:

```php
use PHPUnit\Framework\TestCase;

class CalculatorTest extends TestCase {
    public function testAddition() {
        $calculator = new Calculator();
        $this->assertEquals(4, $calculator->add(2, 2));
    }
}
```

---

## **4. Függőségek kezelése**

- Refaktoráld a kódot, hogy támogassa a tesztelhetőséget (pl. Dependency Injection használata).
- Használj mockokat és stubokat a külső függőségek izolálására. A PHPUnit beépített támogatást nyújt ezekhez:

```php
$mockDatabase = $this->createMock(Database::class);
$mockDatabase->method('findUser')->willReturn(['id' => 1, 'name' => 'John']);
```

---

## **5. Adatbázis és külső szolgáltatások kezelése**

- Használj tesztadatbázist vagy SQLite-ot az adatbázisfüggő funkciók tesztelésére.
- Külső API-k helyett használj mockokat vagy fake objektumokat.

---

## **6. Kód lefedettség mérése**

- Integráld az Xdebugot vagy más kód lefedettség mérő eszközt.
- Futtasd a következő parancsot a kód lefedettség jelentés generálásához:

```bash
./vendor/bin/phpunit --coverage-html coverage/
```

---

## **7. Automatizált tesztelés bevezetése**

- Állíts be egy CI/CD rendszert (pl. GitHub Actions, GitLab CI, Jenkins), amely automatikusan futtatja a teszteket minden commit után.
- Példa GitHub Actions konfigurációra:

```yaml
name: Run Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - uses: shivammathur/setup-php@v2
      with:
        php-version: '8.1'
        extensions: mbstring
    - run: composer install
    - run: ./vendor/bin/phpunit --coverage-text
```

---

## **8. Tesztstratégia kidolgozása**

- Határozd meg, milyen típusú teszteket szeretnél írni: 
  - **Egységtesztek**: Egyedi osztályok és metódusok izolált tesztelése.
  - **Integrációs tesztek**: Több komponens együttműködésének ellenőrzése.
  - **Funkcionális/End-to-End tesztek**: Az alkalmazás teljes viselkedésének ellenőrzése.

---

## **9. Dokumentáció és oktatás**

- Dokumentáld a tesztelési folyamatot és az infrastruktúra használatát.
- Tarts oktatást vagy workshopot a csapat számára, hogy mindenki megértse és alkalmazni tudja az új rendszert.

---

## **10. Folyamatos fejlesztés és karbantartás**

- Folyamatosan bővítsd a tesztkészletet új funkciók hozzáadásakor.
- Rendszeresen frissítsd a függőségeket és tartsd karban az infrastruktúrát.

Ezekkel a lépésekkel fokozatosan kiépítheted a tesztelési infrastruktúrát egy meglévő PHP projektben, miközben minimalizálod az esetleges fennakadásokat vagy problémákat a fejlesztési folyamat során.

Sources