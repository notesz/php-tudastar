# Builder

A Builder pattern egy létrehozási tervezési minta, amely lehetővé teszi komplex objektumok lépésenkénti felépítését. Ez a minta különösen hasznos olyan objektumok létrehozásánál, amelyeknek sok opcionális vagy változó része van.

## Hogyan működik?

1. **Builder interfész**: Definiálja az objektum részeinek létrehozásához szükséges lépéseket.

2. **Concrete Builder (Konkrét Építő)**: Implementálja a Builder interfészt, és megvalósítja az objektum részeinek konkrét létrehozását.

3. **Product (Termék)**: A létrehozandó komplex objektum.

4. **Director (Igazgató)**: Irányítja az objektum építési folyamatát a Builder interfészen keresztül.

## Példa PHP-ban:

```php
// Product
class Car {
    private $parts = [];

    public function addPart($part) {
        $this->parts[] = $part;
    }

    public function showParts() {
        echo "Autó részei: " . implode(', ', $this->parts) . "\n";
    }
}

// Builder interfész
interface CarBuilder {
    public function reset();
    public function setSeats($number);
    public function setEngine($type);
    public function setTripComputer();
    public function setGPS();
    public function getResult(): Car;
}

// Concrete Builder
class SportCarBuilder implements CarBuilder {
    private $car;

    public function reset() {
        $this->car = new Car();
    }

    public function setSeats($number) {
        $this->car->addPart("$number sport ülés");
    }

    public function setEngine($type) {
        $this->car->addPart("$type sport motor");
    }

    public function setTripComputer() {
        $this->car->addPart("Fedélzeti számítógép");
    }

    public function setGPS() {
        $this->car->addPart("GPS navigáció");
    }

    public function getResult(): Car {
        return $this->car;
    }
}

// Director
class CarDirector {
    private $builder;

    public function setBuilder(CarBuilder $builder) {
        $this->builder = $builder;
    }

    public function constructSportsCar() {
        $this->builder->reset();
        $this->builder->setSeats(2);
        $this->builder->setEngine("V8");
        $this->builder->setTripComputer();
        $this->builder->setGPS();
    }
}

// Használat
$director = new CarDirector();
$sportCarBuilder = new SportCarBuilder();

$director->setBuilder($sportCarBuilder);
$director->constructSportsCar();

$sportCar = $sportCarBuilder->getResult();
$sportCar->showParts();
```

## Előnyök:

1. **Lépésenkénti építés**: Lehetővé teszi egy objektum lépésenkénti felépítését.
2. **Kód újrafelhasználás**: Ugyanaz az építési folyamat használható különböző reprezentációk létrehozására.
3. **Komplex objektumok kezelése**: Jól kezeli a sok opcionális paraméterrel rendelkező objektumokat.
4. **Elkülönítés**: Elválasztja az objektum felépítését annak reprezentációjától.

## Hátrányok:

1. **Komplexitás**: Növelheti a kód komplexitását új osztályok és interfészek bevezetésével.
2. **Kötöttség**: A termék struktúrája kötött lehet a Builder interfész által.

A Builder pattern különösen hasznos olyan helyzetekben, ahol egy objektumnak sok konfigurálható opciója van, például egy dokumentum generátor esetében, ahol különböző formátumú dokumentumokat kell létrehozni, vagy egy étterem alkalmazásban, ahol különböző típusú ételeket kell összeállítani.