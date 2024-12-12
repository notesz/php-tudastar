# Layered Pattern (más néven N-Tier Architecture)

A Layered Pattern egy olyan szoftvertervezési minta, amely az alkalmazást logikailag elkülönített rétegekre osztja fel. Ez a megközelítés segít a felelősségek szétválasztásában és a függőségek kezelésében.

 Különösen alkalmas közepes és nagyméretű alkalmazások fejlesztésére, ahol fontos a kód modularitása és karbantarthatósága. A rétegek világos elválasztása lehetővé teszi a fejlesztők számára, hogy az alkalmazás egyes részeire koncentráljanak anélkül, hogy az egész rendszert érintenék.

## Fő jellemzők

- Az alkalmazást különálló, egymásra épülő rétegekre bontja.
- Minden réteg specifikus feladatot lát el és csak a közvetlenül alatta vagy felette lévő réteggel kommunikál.
- A rétegek fizikailag is elkülönülhetnek, különböző szervereken vagy klasztereken futhatnak.

## Tipikus rétegek

### Prezentációs réteg

- Felhasználói felület megjelenítése
- Felhasználói interakciók kezelése

### Alkalmazás réteg

- Alkalmazás munkafolyamatainak koordinálása
- Üzleti logika feldolgozása

### Üzleti logikai réteg

- Alapvető üzleti szabályok és logika implementálása

### Adathozzáférési réteg

- Adatbázis-műveletek kezelése
- Adatok perzisztenciájának biztosítása

## Előnyök

- **Modularitás**: Könnyebb karbantarthatóság és fejleszthetőség
- **Skálázhatóság**: Az egyes rétegek függetlenül skálázhatók
- **Biztonság**: Rétegenként különböző biztonsági protokollok alkalmazhatók
- **Újrafelhasználhatóság**: A rétegek más alkalmazásokban is felhasználhatók

## Gyakorlati példa a Layered Pattern-ra

Az alábbi példa bemutatja, hogyan lehet elkülöníteni a különböző felelősségeket a réteges architektúrában. \
Minden réteg csak a közvetlenül alatta lévő réteggel kommunikál, ami javítja a kód modularitását és karbantarthatóságát.

### Példa struktúra

```
📦 LayeredPattern
 ┣ 📂 Presentation
 ┃ ┗ 📜 UserController.php
 ┣ 📂 Business
 ┃ ┗ 📜 UserService.php
 ┣ 📂 Data
 ┃ ┗ 📜 UserRepository.php
 ┗ 📂 Domain
   ┗ 📜 User.php
```

### Rétegek implementációja

#### Domain réteg

A `User.php` fájl tartalmazza az alapvető User entitást:

```php
<?php

namespace Domain;

class User {
    private $id;
    private $name;
    private $email;

    public function __construct($id, $name, $email) {
        $this->id = $id;
        $this->name = $name;
        $this->email = $email;
    }

    // Getter és setter metódusok...
}
```

#### Data réteg

A `UserRepository.php` fájl kezeli az adatbázis műveleteket:

```php
<?php

namespace Data;

use Domain\User;

class UserRepository {
    public function getUserById($id) {
        // Itt lenne az adatbázis lekérdezés
        return new User($id, "Teszt Felhasználó", "teszt@example.com");
    }

    public function saveUser(User $user) {
        // Itt lenne az adatbázisba mentés logikája
    }
}
```

#### Business réteg

A `UserService.php` fájl tartalmazza az üzleti logikát:

```php
<?php

namespace Business;

use Data\UserRepository;

class UserService {
    private $userRepository;

    public function __construct(UserRepository $userRepository) {
        $this->userRepository = $userRepository;
    }

    public function getUserDetails($id) {
        $user = $this->userRepository->getUserById($id);
        // Itt lehetne további üzleti logika...
        return $user;
    }
}
```

#### Presentation réteg

A `UserController.php` fájl kezeli a HTTP kéréseket:

```php
<?php

namespace Presentation;

use Business\UserService;

class UserController {
    private $userService;

    public function __construct(UserService $userService) {
        $this->userService = $userService;
    }

    public function showUserDetails($id) {
        $user = $this->userService->getUserDetails($id);
        // Itt történne a nézet renderelése...
        echo "Felhasználó neve: " . $user->getName();
    }
}
```

### Használat

A rétegek használatát így lehetne demonstrálni:

```php
<?php

use Data\UserRepository;
use Business\UserService;
use Presentation\UserController;

$userRepository = new UserRepository();
$userService = new UserService($userRepository);
$userController = new UserController($userService);

$userController->showUserDetails(1);
```