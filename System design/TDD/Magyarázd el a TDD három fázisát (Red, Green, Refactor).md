A **Red, Green, Refactor** ciklus a Tesztvezérelt Fejlesztés (TDD) alapvető folyamata, amely három lépésből áll. Ez a megközelítés biztosítja, hogy a kódot mindig tesztek vezéreljék, és az tiszta, jól strukturált legyen. Íme a részletek:

## **1. Red (Piros): Írj egy tesztet, ami elbukik**

- Első lépésként megírsz egy tesztet, amely a fejlesztendő funkció viselkedését definiálja.
- Mivel még nem létezik a funkció implementációja, a tesztnek el kell buknia.
- Ez biztosítja, hogy a teszt valóban ellenőrzi az elvárt viselkedést.

**Cél:** Egyértelműen definiálni az elvárt eredményt és ellenőrizni, hogy a teszt helyesen működik.

**Példa:**

```php
class CalculatorTest extends PHPUnit\Framework\TestCase {
    public function testAddition() {
        $calculator = new Calculator();
        $this->assertEquals(4, $calculator->add(2, 2));
    }
}
```

A `Calculator` osztály és az `add` metódus még nem létezik, így a teszt elbukik.

---

## **2. Green (Zöld): Készítsd el a minimális kódot, hogy a teszt sikeres legyen**

- A cél itt az, hogy csak annyi kódot írj meg, ami szükséges ahhoz, hogy a teszt sikeresen lefusson.
- Nem kell tökéletes vagy végleges megoldást készíteni; az egyszerűségre és gyors eredményre kell törekedni.

**Cél:** A teszt sikeres lefuttatása (zöld állapot elérése).

**Példa:**

```php
class Calculator {
    public function add($a, $b) {
        return $a + $b;
    }
}
```

Ezzel a minimális implementációval a teszt már zöld lesz.

---

## **3. Refactor (Refaktorálás): Javítsd a kódot minőségileg úgy, hogy a tesztek továbbra is sikeresek legyenek**

- Miután a tesztek sikeresen lefutottak, refaktoráld a kódot annak érdekében, hogy tiszta, olvasható és hatékony legyen.
- Fontos, hogy minden refaktorálás után újra lefuttasd a teszteket annak biztosítására, hogy semmi ne törjön el.

**Cél:** A kód optimalizálása anélkül, hogy az funkcionalitása megváltozna.

**Példa:**\
Ha például több matematikai műveletet kell támogatni:

```php
class Calculator {
    public function add($a, $b) {
        return $a + $b;
    }

    public function subtract($a, $b) {
        return $a - $b;
    }
}
```

A refaktorálás során hozzáadhatunk újabb funkciókat vagy javíthatjuk az osztály struktúráját.

---

## Összegzés

A **Red-Green-Refactor** ciklus lényege:

1. **Red:** Írj egy bukó tesztet (ami meghatározza az elvárt viselkedést).
2. **Green:** Implementáld azt a minimális kódot, ami sikeressé teszi a tesztet.
3. **Refactor:** Tisztítsd meg és optimalizáld a kódot úgy, hogy továbbra is minden teszt sikeres maradjon.

Ez az iteratív folyamat segít fenntartani a kód minőségét és biztosítja annak helyes működését minden fejlesztési lépés során.