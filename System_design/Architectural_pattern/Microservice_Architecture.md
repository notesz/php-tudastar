# Microservice Architecture

A Microservice Architecture (microservice architektúra) egy olyan szoftvertervezési megközelítés, amely az alkalmazást kisebb, önálló szolgáltatások gyűjteményeként szervezi meg.

A Microservice Architecture lehetővé teszi a rugalmas, skálázható és könnyen fejleszthető alkalmazások létrehozását, de megfelelő tervezést és infrastruktúrát igényel a hatékony működéshez. Ez az architektúra különösen alkalmas olyan komplex alkalmazásokhoz, ahol gyors fejlesztésre és független szolgáltatás-frissítésekre van szükség.

## Fő jellemzők

- **Moduláris felépítés**: Az alkalmazás kisebb, független szolgáltatásokra van bontva[1][4].
- **Lazán csatolt komponensek**: A szolgáltatások egymástól függetlenül fejleszthetők és telepíthetők[4].
- **Üzleti képességek köré szerveződés**: Minden szolgáltatás egy konkrét üzleti funkcióért felel[4].
- **Technológiai függetlenség**: A szolgáltatások különböző programozási nyelveken és adatbázisokkal implementálhatók[4].

## Előnyök

- **Rugalmasság**: A szolgáltatások külön-külön frissíthetők és skálázhatók[5].
- **Gyorsabb fejlesztés**: Kisebb kódbázisok, könnyebb megérthetőség és kezelhetőség[5].
- **Jobb hibatűrés**: Egy szolgáltatás hibája nem feltétlenül érinti a teljes rendszert[5].
- **Könnyebb skálázhatóság**: Az egyes szolgáltatások igény szerint skálázhatók[5].

## Kihívások

- **Elosztott rendszer komplexitása**: A szolgáltatások közötti kommunikáció és hibakezelés összetettebb[5].
- **Üzemeltetési összetettség**: Több szolgáltatás telepítése és kezelése nagyobb erőforrást igényel[5].
- **Adatkonzisztencia**: Az elosztott adatkezelés kihívásokat jelent a konzisztencia terén[5].

## Implementáció

A mikroszolgáltatások általában könnyűsúlyú protokollokon keresztül kommunikálnak, mint például HTTP/REST API-k. A szolgáltatások tervezésekor fontos a jól definiált interfészek kialakítása és a szolgáltatások közötti függőségek minimalizálása.

## Gyakorlati példa a Microservice Architecture-ra

Ez egy egyszerű Microservice architecture példája PHP-ban. \
A példában két mikroszolgáltatást fogunk létrehozni: egy felhasználói szolgáltatást és egy termék szolgáltatást. Mindkettő külön API-t biztosít és egymástól függetlenül működik.

Ez a példa bemutatja a Microservice-ek alapvető működését:

- Minden szolgáltatás önállóan fut és saját API-t biztosít.
- Az API Gateway központi belépési pontként szolgál és továbbítja a kéréseket.
- A szolgáltatások függetlenül fejleszthetők és skálázhatók.

### Felhasználói szolgáltatás (user-service.php)

```php
<?php

// Felhasználói szolgáltatás
require 'vendor/autoload.php';

use Slim\Factory\AppFactory;
use Psr\Http\Message\ResponseInterface as Response;
use Psr\Http\Message\ServerRequestInterface as Request;

$app = AppFactory::create();

// Felhasználók adatbázisa (egyszerűsített példa)
$users = [
    1 => ['id' => 1, 'name' => 'Kovács János', 'email' => 'kovacs@example.com'],
    2 => ['id' => 2, 'name' => 'Nagy Éva', 'email' => 'nagy@example.com']
];

// Felhasználó lekérdezése ID alapján
$app->get('/users/{id}', function (Request $request, Response $response, array $args) use ($users) {
    $id = $args['id'];
    if (isset($users[$id])) {
        $response->getBody()->write(json_encode($users[$id]));
        return $response->withHeader('Content-Type', 'application/json');
    } else {
        $response->getBody()->write(json_encode(['error' => 'Felhasználó nem található']));
        return $response->withStatus(404)->withHeader('Content-Type', 'application/json');
    }
});

$app->run();
```

### Termék szolgáltatás (product-service.php)

```php
<?php

// Termék szolgáltatás
require 'vendor/autoload.php';

use Slim\Factory\AppFactory;
use Psr\Http\Message\ResponseInterface as Response;
use Psr\Http\Message\ServerRequestInterface as Request;

$app = AppFactory::create();

// Termékek adatbázisa (egyszerűsített példa)
$products = [
    1 => ['id' => 1, 'name' => 'Laptop', 'price' => 299999],
    2 => ['id' => 2, 'name' => 'Okostelefon', 'price' => 199999]
];

// Termék lekérdezése ID alapján
$app->get('/products/{id}', function (Request $request, Response $response, array $args) use ($products) {
    $id = $args['id'];
    if (isset($products[$id])) {
        $response->getBody()->write(json_encode($products[$id]));
        return $response->withHeader('Content-Type', 'application/json');
    } else {
        $response->getBody()->write(json_encode(['error' => 'Termék nem található']));
        return $response->withStatus(404)->withHeader('Content-Type', 'application/json');
    }
});

$app->run();
```

### API Gateway (api-gateway.php)

Az API Gateway egy központi belépési pont, amely továbbítja a kéréseket a megfelelő mikroszolgáltatásokhoz:

```php
<?php

// API Gateway
require 'vendor/autoload.php';

use Slim\Factory\AppFactory;
use Psr\Http\Message\ResponseInterface as Response;
use Psr\Http\Message\ServerRequestInterface as Request;
use GuzzleHttp\Client;

$app = AppFactory::create();
$client = new Client();

// Felhasználói szolgáltatás proxy
$app->get('/users/{id}', function (Request $request, Response $response, array $args) use ($client) {
    $userResponse = $client->request('GET', 'http://localhost:8001/users/' . $args['id']);
    $response->getBody()->write($userResponse->getBody());
    return $response->withHeader('Content-Type', 'application/json');
});

// Termék szolgáltatás proxy
$app->get('/products/{id}', function (Request $request, Response $response, array $args) use ($client) {
    $productResponse = $client->request('GET', 'http://localhost:8002/products/' . $args['id']);
    $response->getBody()->write($productResponse->getBody());
    return $response->withHeader('Content-Type', 'application/json');
});

$app->run();
```

### Használat

1. Telepítsd a szükséges függőségeket:
   ```bash
   composer require slim/slim slim/psr7 guzzlehttp/guzzle
   ```

2. Indítsd el a szolgáltatásokat külön-külön terminálokban:
   ```bash
   php -S localhost:8001 user-service.php
   php -S localhost:8002 product-service.php
   php -S localhost:8000 api-gateway.php
   ```

3. Teszteld a szolgáltatásokat:
   ```bash
   curl http://localhost:8000/users/1
   curl http://localhost:8000/products/2
   ```