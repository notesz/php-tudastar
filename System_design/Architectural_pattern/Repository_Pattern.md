# Repository Pattern

A Repository Pattern egy szoftvertervezési minta, amely a [Domain-Driven Design](../Software_Design_Principles/DDD.md) részeként vált népszerűvé. Fő célja az adathozzáférési logika központosítása és elkülönítése az üzleti logikától. A minta lényege:

## Fő jellemzők

- Absztrakciót biztosít az adatok perzisztenciájához
- Elválasztja az adathozzáférési réteget a domain modell rétegétől
- Egyszerű interfészt biztosít az adatok kezeléséhez (hozzáadás, lekérdezés, módosítás, törlés)

## Működése

- A repository egy közvetítő rétegként működik az alkalmazás üzleti logikája és az adattárolás között
- Az üzleti logika a repository interfészén keresztül fér hozzá az adatokhoz, nem kell foglalkoznia az adatbázis-kapcsolatokkal vagy lekérdezésekkel

## Előnyök

- Javítja a kód karbantarthatóságát és tesztelhetőségét
- Lazán csatolt komponenseket eredményez
- Lehetővé teszi a domain objektumok perzisztencia-függetlenségét
- Megkönnyíti az adatforrások cseréjét vagy migrációját

## Implementáció

A Repository Pattern általában három fő komponensből áll:

1. Repository interfész: definiálja az adatműveleteket
2. Repository implementáció: megvalósítja az interfészt és kezeli az adathozzáférést
3. Entitás modell: reprezentálja az üzleti entitásokat

A repository-k általában modell-specifikusak, azaz minden entitáshoz külön repository tartozik, ami jobban tükrözi a domain nyelvezetét és rugalmasabb megoldást biztosít.

## Gyakorlati példa a Repository Pattern-ra

Ez egy egyszerű példa a Repository Pattern implementációjára PHP-ban.

A példában egy egyszerű felhasználókezelő rendszert fogunk létrehozni, ahol jól láthatók a Repository Pattern fő elemei:

1. A `User` entitás reprezentálja az üzleti objektumot.
2. A `UserRepositoryInterface` definiálja a műveletek szerződését.
3. A `UserRepository` kezeli az adathozzáférési logikát.
4. Az üzleti logika a repository-n keresztül fér hozzá az adatokhoz, nem foglalkozik az adatbázis-műveletekkel.

## 1. Entitás modell

Először hozzuk létre a `User` entitást:

```php
<?php

class User
{
    private $id;
    private $name;
    private $email;

    public function __construct($id, $name, $email)
    {
        $this->id = $id;
        $this->name = $name;
        $this->email = $email;
    }

    // Getter metódusok
    public function getId() { return $this->id; }
    public function getName() { return $this->name; }
    public function getEmail() { return $this->email; }

    // Setter metódusok
    public function setName($name) { $this->name = $name; }
    public function setEmail($email) { $this->email = $email; }
}
```

## 2. Repository interfész

Most definiáljuk a `UserRepositoryInterface` interfészt:

```php
<?php

interface UserRepositoryInterface
{
    public function find($id);
    public function findAll();
    public function save(User $user);
    public function delete($id);
}
```

## 3. Repository implementáció

Implementáljuk a `UserRepository`-t:

```php
<?php

class UserRepository implements UserRepositoryInterface
{
    private $db;

    public function __construct(PDO $db)
    {
        $this->db = $db;
    }

    public function find($id)
    {
        $statement = $this->db->prepare("SELECT * FROM users WHERE id = :id");
        $statement->execute(['id' => $id]);
        $userData = $statement->fetch(PDO::FETCH_ASSOC);

        if (!$userData) {
            return null;
        }

        return new User($userData['id'], $userData['name'], $userData['email']);
    }

    public function findAll()
    {
        $statement = $this->db->query("SELECT * FROM users");
        $usersData = $statement->fetchAll(PDO::FETCH_ASSOC);

        $users = [];
        foreach ($usersData as $userData) {
            $users[] = new User($userData['id'], $userData['name'], $userData['email']);
        }

        return $users;
    }

    public function save(User $user)
    {
        if ($user->getId()) {
            // Frissítés
            $statement = $this->db->prepare("UPDATE users SET name = :name, email = :email WHERE id = :id");
            $statement->execute([
                'id' => $user->getId(),
                'name' => $user->getName(),
                'email' => $user->getEmail()
            ]);
        } else {
            // Új felhasználó létrehozása
            $statement = $this->db->prepare("INSERT INTO users (name, email) VALUES (:name, :email)");
            $statement->execute([
                'name' => $user->getName(),
                'email' => $user->getEmail()
            ]);
            // Az új ID beállítása
            $user = new User($this->db->lastInsertId(), $user->getName(), $user->getEmail());
        }

        return $user;
    }

    public function delete($id)
    {
        $statement = $this->db->prepare("DELETE FROM users WHERE id = :id");
        $statement->execute(['id' => $id]);
    }
}
```

## 4. Használat

Végül nézzük meg, hogyan használhatjuk ezt a repository-t:

```php
<?php

// Adatbázis kapcsolat létrehozása
$pdo = new PDO('mysql:host=localhost;dbname=testdb', 'username', 'password');

// Repository példányosítása
$userRepository = new UserRepository($pdo);

// Új felhasználó létrehozása
$newUser = new User(null, 'Kovács János', 'kovacs@example.com');
$savedUser = $userRepository->save($newUser);
echo "Új felhasználó ID-je: " . $savedUser->getId() . "\n";

// Felhasználó keresése
$user = $userRepository->find($savedUser->getId());
if ($user) {
    echo "Talált felhasználó: " . $user->getName() . "\n";
} else {
    echo "Felhasználó nem található.\n";
}

// Összes felhasználó listázása
$allUsers = $userRepository->findAll();
foreach ($allUsers as $user) {
    echo $user->getName() . " - " . $user->getEmail() . "\n";
}

// Felhasználó törlése
$userRepository->delete($savedUser->getId());
echo "Felhasználó törölve.\n";
```