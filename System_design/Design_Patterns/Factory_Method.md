# Factory Method

A Factory Method pattern egy létrehozási tervezési minta, amely lehetővé teszi objektumok létrehozását anélkül, hogy előre meghatároznánk a pontos osztályt. Ez a minta különösen hasznos, amikor a kódot el szeretnénk választani a konkrét implementációtól.

## Hogyan működik?

1. **Absztrakt Termék**: Definiál egy interfészt vagy absztrakt osztályt a létrehozandó objektumokhoz.

2. **Konkrét Termékek**: Az Absztrakt Termék különböző implementációi.

3. **Absztrakt Gyár**: Deklarál egy absztrakt metódust (a Factory Method-ot) az objektumok létrehozására.

4. **Konkrét Gyárak**: Az Absztrakt Gyár leszármazottai, amelyek implementálják a Factory Method-ot, és konkrét Termék objektumokat hoznak létre.

## Példa PHP-ban:

```php
// Absztrakt Termék
interface Vehicle {
    public function drive();
}

// Konkrét Termékek
class Car implements Vehicle {
    public function drive() {
        return "Autót vezetünk";
    }
}

class Bike implements Vehicle {
    public function drive() {
        return "Biciklizünk";
    }
}

// Absztrakt Gyár
abstract class VehicleFactory {
    abstract public function createVehicle(): Vehicle;

    public function driveVehicle() {
        $vehicle = $this->createVehicle();
        return $vehicle->drive();
    }
}

// Konkrét Gyárak
class CarFactory extends VehicleFactory {
    public function createVehicle(): Vehicle {
        return new Car();
    }
}

class BikeFactory extends VehicleFactory {
    public function createVehicle(): Vehicle {
        return new Bike();
    }
}

// Használat
$carFactory = new CarFactory();
echo $carFactory->driveVehicle() . "\n"; // Kimenet: Autót vezetünk

$bikeFactory = new BikeFactory();
echo $bikeFactory->driveVehicle() . "\n"; // Kimenet: Biciklizünk
```

## Előnyök:

1. **Rugalmasság**: Könnyen bővíthető új termékekkel anélkül, hogy a meglévő kódot módosítanánk.
2. **Lazán csatolt kód**: A kliens kód független a konkrét osztályoktól.
3. **Egységbe zárás**: A termék létrehozásának logikája egy helyen van.

## Hátrányok:

1. **Komplexitás**: Több osztályt és interfészt kell létrehozni, ami bonyolultabbá teheti a kódot.
2. **Túlzott használat**: Nem minden objektum létrehozásához szükséges Factory Method.

A Factory Method pattern különösen hasznos, amikor egy osztálynak nem kell tudnia, hogy pontosan milyen osztályú objektumokat kell létrehoznia, vagy amikor egy osztály azt szeretné, hogy az alosztályai határozzák meg a létrehozandó objektumokat.