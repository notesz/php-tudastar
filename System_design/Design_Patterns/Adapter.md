# Adapter

Az **Adapter pattern** (Adapter minta) egy szerkezeti tervezési minta, amely lehetővé teszi, hogy két inkompatibilis interfész együttműködjön. Az Adapter minta "híd" szerepet tölt be a meglévő kód és az új interfészek között, így lehetővé téve a régi és az új rendszerek közötti integrációt.

## Hogyan működik?

1. **Target (Cél)**: Ez az interfész, amelyet a kliens használni szeretne. Az Adapter minta célja, hogy biztosítsa, hogy a meglévő osztályok ezt az interfészt tudják implementálni.

2. **Adaptee (Alkalmazott)**: Ez az osztály, amelynek a funkcionalitását szeretnénk használni, de nem felel meg a Target interfésznek.

3. **Adapter**: Ez az osztály implementálja a Target interfészt és tartalmaz egy referenciát az Adaptee objektumra. Az Adapter felelős azért, hogy az Adaptee metódusait a Target interfész által elvárt módon hívja meg.

## Példa PHP-ban:

```php
// Target interface
interface Target {
    public function request();
}

// Adaptee class
class Adaptee {
    public function specificRequest() {
        return "Adaptee: Specific request.";
    }
}

// Adapter class
class Adapter implements Target {
    private $adaptee;

    public function __construct(Adaptee $adaptee) {
        $this->adaptee = $adaptee;
    }

    public function request() {
        // Az Adaptee metódusának hívása
        return $this->adaptee->specificRequest();
    }
}

// Használat
function clientCode(Target $target) {
    echo $target->request();
}

// A kliens kód használja az Adaptert
$adaptee = new Adaptee();
$adapter = new Adapter($adaptee);
clientCode($adapter); // Kimenet: Adaptee: Specific request.
```

## Előnyök:

1. **Rugalmasság**: Lehetővé teszi a régi kód új interfészekkel való használatát anélkül, hogy a meglévő kódot módosítani kellene.
2. **Kód újrafelhasználás**: A meglévő osztályok könnyen integrálhatók új rendszerekbe.
3. **Könnyen bővíthető**: Új adapterek létrehozása egyszerű, ha új interfészeket kell támogatni.

## Hátrányok:

1. **Komplexitás**: Növelheti a kód komplexitását, mivel több osztályt kell kezelni.
2. **Teljesítmény**: Az adapterek használata extra réteget adhat hozzá, ami kissé lelassíthatja a rendszert (bár ez általában elhanyagolható).

Az Adapter pattern különösen hasznos olyan helyzetekben, amikor régi kódot szeretnénk integrálni új rendszerbe vagy amikor különböző rendszerek közötti kommunikációt kell megvalósítani, például API-k integrálásakor vagy különböző könyvtárak használatakor.