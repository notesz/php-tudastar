# Hogyan írnál teszteket egy egyszerű API végponthoz TDD megközelítéssel

A TDD (Test-Driven Development) megközelítéssel egy egyszerű API végpont tesztelése során a következő lépéseket követnénk:

## 1. A teszt megtervezése

Először határozzuk meg, mit várunk el az API végponttól. Tegyük fel, hogy egy `/api/users/{id}` GET végpontot szeretnénk létrehozni, amely visszaad egy felhasználót az ID alapján.

## 2. A teszt megírása

Hozzunk létre egy `UserApiTest.php` fájlt:

```php
use PHPUnit\Framework\TestCase;

class UserApiTest extends TestCase
{
    public function testGetUserById()
    {
        $client = new Client();
        $response = $client->get('/api/users/1');

        $this->assertEquals(200, $response->getStatusCode());
        $this->assertJson($response->getBody());

        $data = json_decode($response->getBody(), true);
        $this->assertArrayHasKey('id', $data);
        $this->assertArrayHasKey('name', $data);
        $this->assertEquals(1, $data['id']);
    }

    public function testGetNonExistentUser()
    {
        $client = new Client();
        $response = $client->get('/api/users/999');

        $this->assertEquals(404, $response->getStatusCode());
    }
}
```

## 3. A teszt futtatása (Red fázis)

Futtassuk le a tesztet. Természetesen ez most elbukik, hiszen még nem implementáltuk az API-t.

## 4. Az API implementálása (Green fázis)

Most implementáljuk az API végpontot, például egy Slim keretrendszerrel:

```php
$app->get('/api/users/{id}', function (Request $request, Response $response, array $args) {
    $id = $args['id'];
    $user = $this->userRepository->find($id);

    if (!$user) {
        return $response->withStatus(404);
    }

    return $response->withJson([
        'id' => $user->getId(),
        'name' => $user->getName()
    ]);
});
```

## 5. A teszt újbóli futtatása

Most futtassuk újra a tesztet. Ha mindent jól csináltunk, a teszt sikeresen lefut.

## 6. Refaktorálás (ha szükséges)

Ha szükséges, végezzünk refaktorálást a kódon, miközben biztosítjuk, hogy a tesztek továbbra is sikeresek maradjanak.

## 7. További tesztek hozzáadása

Folytassuk a folyamatot további tesztek hozzáadásával, például:

```php
public function testInvalidUserId()
{
    $client = new Client();
    $response = $client->get('/api/users/invalid');

    $this->assertEquals(400, $response->getStatusCode());
}
```

Ez a teszt azt ellenőrzi, hogy az API megfelelően kezeli-e az érvénytelen felhasználói azonosítókat.

## 8. Az API bővítése a új teszt alapján

Implementáljuk az új követelményt az API-ban:

```php
$app->get('/api/users/{id}', function (Request $request, Response $response, array $args) {
    $id = $args['id'];
    if (!is_numeric($id)) {
        return $response->withStatus(400);
    }
    // ... (a korábbi implementáció folytatása)
});
```

Ez a TDD ciklus folytatódik, ahogy új funkciókat adunk hozzá vagy módosítjuk a meglévőket. Minden változtatás előtt megírjuk a tesztet, majd implementáljuk a funkciót, és végül refaktoráljuk a kódot, ha szükséges.