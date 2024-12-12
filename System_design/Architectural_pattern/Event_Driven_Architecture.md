# Event Driven Architecture (Event Driven Design & Message Driven Design)

Az Event Driven Architecture (EDA) egy olyan szoftvertervezési minta, amely események előállítása, észlelése és feldolgozása köré szervezi a rendszer működését. Az EDA lényege, hogy a rendszer komponensei eseményeken keresztül kommunikálnak egymással, ami rugalmas és skálázható architektúrát eredményez.

## Fő jellemzők:

- Esemény-központúság: A rendszer működését események vezérlik, amelyek lehetnek állapotváltozások vagy fontos történések.
- Lazán csatolt komponensek: Az eseményeket előállító és feldolgozó komponensek függetlenek egymástól.
- Aszinkron kommunikáció: Az események feldolgozása aszinkron módon történik, ami javítja a rendszer válaszidejét és skálázhatóságát.

## Előnyök

- Valós idejű reagálás: A rendszer képes azonnal reagálni a bekövetkező eseményekre.
- Skálázhatóság: A komponensek függetlensége miatt könnyen bővíthető a rendszer.
- Rugalmasság: Új funkciók könnyen integrálhatók új esemény-előállítók vagy -fogyasztók hozzáadásával.
- Hibatűrés: Az események tárolhatók és később újra feldolgozhatók, ami növeli a rendszer megbízhatóságát.

Az Event Driven Architecture különösen alkalmas olyan rendszerekhez, ahol fontos a valós idejű adatfeldolgozás és a gyors reagálás a változásokra, például IoT alkalmazásokban, pénzügyi rendszerekben vagy e-kereskedelmi platformokon.

## Gyakorlati példa a Event Driven Architecture-ra

A példában egy egyszerű eseménykezelő rendszert fogunk létrehozni, amely demonstrálja az esemény-előállítás, -továbbítás és -feldolgozás folyamatát.

A példa bemutatja az alapvető működést:

1. Az `OrderProcessor` feldolgozza a rendelést és létrehoz egy eseményt.
2. Az `EventDispatcher` továbbítja az eseményt a regisztrált hallgatóknak.
3. Az `EmailNotifier` és `InventoryManager` reagálnak az eseményre és végrehajtják a megfelelő műveleteket.

### Esemény osztály

Először hozzunk létre egy alapvető `Event` osztályt:

```php
<?php

class Event
{
    private $name;
    private $data;

    public function __construct(string $name, array $data = [])
    {
        $this->name = $name;
        $this->data = $data;
    }

    public function getName(): string
    {
        return $this->name;
    }

    public function getData(): array
    {
        return $this->data;
    }
}
```

### Eseménykezelő osztály

Most hozzunk létre egy `EventDispatcher` osztályt, amely kezeli az eseményeket és a hozzájuk tartozó hallgatókat:

```php
<?php

class EventDispatcher
{
    private $listeners = [];

    public function addListener(string $eventName, callable $listener): void
    {
        $this->listeners[$eventName][] = $listener;
    }

    public function dispatch(Event $event): void
    {
        $eventName = $event->getName();
        if (isset($this->listeners[$eventName])) {
            foreach ($this->listeners[$eventName] as $listener) {
                call_user_func($listener, $event);
            }
        }
    }
}
```

### Esemény-előállító osztály

Hozzunk létre egy példa esemény-előállító osztályt:

```php
<?php

class OrderProcessor
{
    private $eventDispatcher;

    public function __construct(EventDispatcher $eventDispatcher)
    {
        $this->eventDispatcher = $eventDispatcher;
    }

    public function processOrder(array $orderData): void
    {
        // Rendelés feldolgozása...
        echo "Rendelés feldolgozva: " . $orderData['id'] . "\n";

        // Esemény létrehozása és továbbítása
        $event = new Event('order.processed', $orderData);
        $this->eventDispatcher->dispatch($event);
    }
}
```

### Esemény-hallgató osztályok

Most hozzunk létre néhány esemény-hallgató osztályt:

```php
<?php

class EmailNotifier
{
    public function sendOrderConfirmation(Event $event): void
    {
        $orderData = $event->getData();
        echo "E-mail értesítés küldése a rendelésről: " . $orderData['id'] . "\n";
    }
}

class InventoryManager
{
    public function updateStock(Event $event): void
    {
        $orderData = $event->getData();
        echo "Készlet frissítése a rendelés alapján: " . $orderData['id'] . "\n";
    }
}
```

### Használat

Végül, használjuk az elkészített komponenseket:

```php
<?php

// Eseménykezelő létrehozása
$eventDispatcher = new EventDispatcher();

// Hallgatók regisztrálása
$emailNotifier = new EmailNotifier();
$inventoryManager = new InventoryManager();

$eventDispatcher->addListener('order.processed', [$emailNotifier, 'sendOrderConfirmation']);
$eventDispatcher->addListener('order.processed', [$inventoryManager, 'updateStock']);

// Rendelésfeldolgozó létrehozása
$orderProcessor = new OrderProcessor($eventDispatcher);

// Rendelés feldolgozása
$orderData = ['id' => '12345', 'total' => 1000];
$orderProcessor->processOrder($orderData);
```