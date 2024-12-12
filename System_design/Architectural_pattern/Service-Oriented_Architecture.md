# Service-Oriented Architecture (SOA)

A Service-Oriented Architecture (SOA), azaz szolgáltatásorientált architektúra, egy szoftverfejlesztési modell, amely újrafelhasználható szolgáltatásokra épül.

## Fő jellemzői

- Szolgáltatásokra bontja a rendszert, ahol minden szolgáltatás egy konkrét üzleti funkciót valósít meg.
- A szolgáltatások platformfüggetlenek és különböző nyelveken íródhatnak.
- Szabványos kommunikációs protokollokat használ a szolgáltatások közötti adatcserére.
- A szolgáltatások lazán csatoltak és függetlenek egymástól.
- Lehetővé teszi a szolgáltatások újrafelhasználását különböző alkalmazásokban.

A SOA előnyei közé tartozik a gyorsabb fejlesztés, a könnyebb karbantarthatóság, a jobb skálázhatóság és az interoperabilitás elősegítése. A szolgáltatások egy szolgáltatási sínen (ESB) keresztül kommunikálnak egymással, ami biztosítja az üzenetközvetítést és a különböző platformok közötti együttműködést.

## Gyakorlati példa a Service-Oriented Architecture-ra

Ez egy egyszerű példa a Service-Oriented Architecture (SOA) megvalósítására PHP-ban. \
Ebben a példában létrehozunk két szolgáltatást: 
- egy felhasználói szolgáltatást és egy rendelési szolgáltatást, valamint 
- egy szolgáltatás regisztert, amely kezeli ezeket a szolgáltatásokat.

A példa bemutatja a SOA alapvető koncepcióit:

1. **Szolgáltatások**: Különálló, újrafelhasználható komponensek (UserService, OrderService).
2. **Lazán csatolt komponensek**: A szolgáltatások függetlenek egymástól és a ServiceInterface-en keresztül kommunikálnak.
3. **Szolgáltatás regiszter**: Központi hely a szolgáltatások kezelésére és elérésére.
4. **Szabványos interfész**: Minden szolgáltatás ugyanazt az interfészt implementálja.

### 1. Szolgáltatás interfész

Először definiáljunk egy interfészt a szolgáltatásokhoz:

```php
<?php

interface ServiceInterface
{
    public function execute($data);
}
```

### 2. Felhasználói szolgáltatás

```php
<?php

class UserService implements ServiceInterface
{
    public function execute($data)
    {
        // Felhasználó adatainak lekérdezése
        return [
            'id' => $data['id'],
            'name' => 'Teszt Felhasználó',
            'email' => 'teszt@example.com'
        ];
    }
}
```

### 3. Rendelési szolgáltatás

```php
<?php

class OrderService implements ServiceInterface
{
    public function execute($data)
    {
        // Rendelés létrehozása
        return [
            'order_id' => uniqid(),
            'user_id' => $data['user_id'],
            'total' => $data['total']
        ];
    }
}
```

### 4. Szolgáltatás regiszter

```php
<?php

class ServiceRegistry
{
    private $services = [];

    public function register($name, ServiceInterface $service)
    {
        $this->services[$name] = $service;
    }

    public function get($name)
    {
        if (!isset($this->services[$name])) {
            throw new Exception("Service not found: $name");
        }
        return $this->services[$name];
    }
}
```

### 5. Szolgáltatás használata

Most nézzük meg, hogyan használhatjuk ezeket a szolgáltatásokat:

```php
<?php

// Szolgáltatások létrehozása
$userService = new UserService();
$orderService = new OrderService();

// Szolgáltatás regiszter létrehozása és szolgáltatások regisztrálása
$registry = new ServiceRegistry();
$registry->register('user', $userService);
$registry->register('order', $orderService);

// Szolgáltatások használata
try {
    // Felhasználó lekérdezése
    $userData = $registry->get('user')->execute(['id' => 1]);
    echo "Felhasználó: " . $userData['name'] . "\n";

    // Rendelés létrehozása
    $orderData = $registry->get('order')->execute([
        'user_id' => $userData['id'],
        'total' => 100.00
    ]);
    echo "Rendelés azonosító: " . $orderData['order_id'] . "\n";
} catch (Exception $e) {
    echo "Hiba: " . $e->getMessage() . "\n";
}
```

Valós SOA implementációban további elemeket is figyelembe vennénk:

- **Szolgáltatási sín (ESB)**: Komplex rendszerekben ez kezelné a szolgáltatások közötti kommunikációt.
- **Biztonság**: Hitelesítés és jogosultságkezelés a szolgáltatások eléréséhez.
- **Tranzakciókezelés**: Elosztott tranzakciók kezelése több szolgáltatás között.
- **Monitorozás és naplózás**: A szolgáltatások teljesítményének és hibáinak nyomon követése.