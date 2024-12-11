# Mi az adatforrások (data providers) szerepe a PHPUnit-ben

Az adatforrások (data providers) a PHPUnit egyik hasznos funkciója, amely lehetővé teszi, hogy ugyanazt a tesztet többféle bemeneti adattal futtassuk le. Ez különösen hasznos, amikor egy metódus viselkedését különböző bemeneti értékekkel szeretnénk tesztelni.

## Az adatforrások előnyei

1. **Kód újrafelhasználás**: Nem kell több hasonló tesztmetódust írni különböző bemeneti értékekhez.
2. **Átláthatóság**: A tesztesetek és a hozzájuk tartozó adatok elkülönülnek, ami javítja a kód olvashatóságát.
3. **Könnyű bővíthetőség**: Új tesztesetek hozzáadása egyszerűen megoldható az adatforrás bővítésével.
4. **Hatékonyság**: Csökkenti a redundáns kódot és megkönnyíti a tesztek karbantartását.

## Hogyan működik?

Az adatforrás egy külön metódus, amely egy tömböt vagy iterálható objektumot ad vissza. Minden elem ebben a tömbben egy teszteset adatait tartalmazza.

## Példa

Tegyük fel, hogy van egy `Calculator` osztályunk egy `add` metódussal:

```php
class Calculator {
    public function add($a, $b) {
        return $a + $b;
    }
}
```

Íme egy példa az adatforrás használatára a tesztelésben:

```php
use PHPUnit\Framework\TestCase;

class CalculatorTest extends TestCase {
    /**
     * @dataProvider additionProvider
     */
    public function testAdd($a, $b, $expected) {
        $calculator = new Calculator();
        $this->assertEquals($expected, $calculator->add($a, $b));
    }

    public function additionProvider() {
        return [
            [0, 0, 0],
            [1, 1, 2],
            [-1, 1, 0],
            [1.5, 2.5, 4],
        ];
    }
}
```

Ebben a példában:

1. Az `additionProvider` metódus szolgál adatforrásként.
2. A `@dataProvider` annotáció köti össze a tesztmetódust az adatforrással.
3. Az adatforrás minden sora egy külön tesztesetnek felel meg.
4. A PHPUnit automatikusan végigmegy az összes adatsoron, és mindegyikkel lefuttatja a tesztet.