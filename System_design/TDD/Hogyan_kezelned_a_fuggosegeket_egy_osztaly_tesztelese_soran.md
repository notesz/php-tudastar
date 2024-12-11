# Hogyan kezelnéd a függőségeket (dependencies) egy osztály tesztelése során

A függőségek kezelése kulcsfontosságú az egységtesztek írása során, különösen amikor komplex osztályokat tesztelünk. Íme néhány hatékony módszer a függőségek kezelésére PHP-ban:

## 1. Dependency Injection (Függőség Befecskendezés)

Ez az egyik leghatékonyabb módszer a függőségek kezelésére. Ahelyett, hogy az osztály maga hozná létre a függőségeit, kívülről kapja meg azokat.

**Példa:**

```php
class UserService {
    private $database;

    public function __construct(Database $database) {
        $this->database = $database;
    }

    public function getUser($id) {
        return $this->database->findUser($id);
    }
}

class UserServiceTest extends PHPUnit\Framework\TestCase {
    public function testGetUser() {
        $mockDatabase = $this->createMock(Database::class);
        $mockDatabase->method('findUser')->willReturn(['id' => 1, 'name' => 'John']);

        $userService = new UserService($mockDatabase);
        $user = $userService->getUser(1);

        $this->assertEquals('John', $user['name']);
    }
}
```

## 2. Mock Objects (Utánzó Objektumok)

A PHPUnit beépített mock objektum generátorral rendelkezik, amely lehetővé teszi a függőségek szimulálását.

```php
public function testSendEmail() {
    $mockMailer = $this->createMock(Mailer::class);
    $mockMailer->expects($this->once())
               ->method('send')
               ->with('test@example.com', 'Test Subject', 'Test Body')
               ->willReturn(true);

    $notificationService = new NotificationService($mockMailer);
    $result = $notificationService->notifyUser('test@example.com');

    $this->assertTrue($result);
}
```

## 3. Stub Classes (Csonk Osztályok)

Egyszerűbb esetekben használhatunk stub osztályokat, amelyek a valódi osztályok egyszerűsített változatai.

```php
class StubLogger implements LoggerInterface {
    public function log($message) {
        // Nem csinál semmit
    }
}

public function testProcessWithLogger() {
    $stubLogger = new StubLogger();
    $processor = new DataProcessor($stubLogger);
    $result = $processor->process(['data']);
    $this->assertNotEmpty($result);
}
```

## 4. Test Doubles (Teszt Dublőrök)

A PHPUnit lehetővé teszi különböző típusú teszt dublőrök használatát, mint például dummy, stub, spy, mock és fake objektumok.

```php
public function testCalculateTotal() {
    $stubProduct = $this->createStub(Product::class);
    $stubProduct->method('getPrice')->willReturn(10.00);

    $cart = new ShoppingCart();
    $cart->addItem($stubProduct, 2);

    $this->assertEquals(20.00, $cart->getTotal());
}
```

## 5. Service Locator Pattern

Bár nem annyira ajánlott, mint a Dependency Injection, néha használható a Service Locator minta is.

```php
class ServiceLocator {
    private static $services = [];

    public static function set($name, $service) {
        self::$services[$name] = $service;
    }

    public static function get($name) {
        return self::$services[$name] ?? null;
    }
}

// Tesztben:
ServiceLocator::set('database', $mockDatabase);
```

A függőségek megfelelő kezelése lehetővé teszi, hogy az egységtesztek valóban izoláltak legyenek, és csak az adott osztály vagy metódus működését teszteljék, függetlenül a külső rendszerektől vagy szolgáltatásoktól.