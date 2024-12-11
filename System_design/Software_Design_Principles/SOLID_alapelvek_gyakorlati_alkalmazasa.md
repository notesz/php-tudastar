# SOLID alapelvek gyakorlati alkalmazása

A SOLID elvek gyakorlati alkalmazására számos példa hozható fel:

## Single Responsibility Principle (SRP)

Ahelyett, hogy egy `User` osztály kezelné a felhasználói adatokat és az adatbázis műveleteket is, hozzunk létre külön osztályokat:

- `User` osztály: csak a felhasználói adatok tárolására
- `UserRepository` osztály: az adatbázis műveletek kezelésére

## Open/Closed Principle (OCP)

Használjunk interfészeket a viselkedés definiálására:

```php
interface IMessageService {
    public function Send(string $message);
}

class EmailService implements IMessageService {
    public function Send(string $message) {
        // E-mail küldés implementációja
    }
}

class SmsService implements IMessageService {
    public function Send(string $message) {
        // SMS küldés implementációja
    }
}
```

Így új üzenetküldési módokat adhatunk hozzá a meglévő kód módosítása nélkül.

## Liskov Substitution Principle (LSP)

Tervezzük úgy az öröklődési hierarchiát, hogy az alosztályok valóban helyettesíthetők legyenek a szülőosztályokkal. Például egy `Rectangle` és `Square` osztály esetében:

```php
class Rectangle {
    protected $width;
    protected $height;

    public function setWidth($width) {
        $this->width = $width;
    }

    public function setHeight($height) {
        $this->height = $height;
    }
}

class Square extends Rectangle {
    public function setWidth($width) {
        $this->width = $this->height = $width;
    }

    public function setHeight($height) {
        $this->width = $this->height = $height;
    }
}
```

## Interface Segregation Principle (ISP)

Hozzunk létre kisebb, specifikus interfészeket:

```php
interface Printable {
    public function print();
}

interface Scannable {
    public function scan();
}

class AllInOnePrinter implements Printable, Scannable {
    public function print() { /* ... */ }
    public function scan() { /* ... */ }
}

class SimplePrinter implements Printable {
    public function print() { /* ... */ }
}
```

## Dependency Inversion Principle (DIP)

Használjunk függőség befecskendezést:

```php
class MessageSender {
    private $messageService;

    public function __construct(IMessageService $service) {
        $this->messageService = $service;
    }

    public function sendMessage(string $message) {
        $this->messageService->Send($message);
    }
}
```

Ezek a példák segítenek megérteni, hogyan alkalmazhatók a SOLID elvek a gyakorlatban, elősegítve a rugalmas, karbantartható és bővíthető kód létrehozását