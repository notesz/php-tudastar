# PASETO

A PASETO (Platform-Agnostic SEcurity TOkens) egy új szabvány biztonságos, állapotmentes tokenek létrehozására, amelyet a JSON Web Tokenek (JWT) hiányosságainak kiküszöbölésére fejlesztettek ki. \
A PASETO elsődleges célja a biztonság, egyszerűség és könnyű használhatóság biztosítása a modern alkalmazások számára.

## Főbb jellemzői

- **Biztonságosabb alternatíva**: A PASETO úgy lett kialakítva, hogy kiküszöbölje a JWT-k gyakori biztonsági problémáit, például az algoritmus-összezavarást.

- **Egyszerűbb használat**: A fejlesztőknek nem kell bonyolult kriptográfiai döntéseket hozniuk, mivel a PASETO előre meghatározott, erős kriptográfiai algoritmusokat használ.

- **Verziókezelés**: A PASETO különböző verziókkal rendelkezik, amelyek mindegyike specifikus kriptográfiai szabványokra és felhasználási esetekre van tervezve.

## A token felépítése

A PASETO token három vagy négy részből áll, amelyeket pontokkal választanak el:

```
<version>.<purpose>.<payload>.<footer>
```

- **version**: Jelzi a token generálásához használt protokoll verzióját.
- **purpose**: Lehet "local" (titkosított) vagy "public" (aláírt).
- **payload**: Tartalmazza a claims-eket és adatokat.
- **footer**: Opcionális rész, nem érzékeny információkkal.

## Típusai

1. **Local (szimmetrikus) PASETO**: Titkosított tokenek, amelyeket egy megosztott titkos kulccsal hoznak létre és dekódolnak.
2. **Public (aszimmetrikus) PASETO**: Nem titkosított, de digitálisan aláírt tokenek, amelyeket nyilvános kulcsú kriptográfiával ellenőriznek.

## Gyakorlati példa a PASETO működésére

Az alábbi példa bemutatja, hogyan implementálhatjuk a PASETO-t API útvonalaink védelmére.

### PASETO implementálása

A példában szereplő kódhoz a [paragonie/paseto](https://packagist.org/packages/paragonie/paseto) csomag telepítése szükséges.

```bash
composer require paragonie/paseto
```

### Secret key létrehozása

Hozzunk létre a secret key-t a tokenek aláírásához:

```php
use ParagonIE\Paseto\Keys\SymmetricKey;

$secretKey = new SymmetricKey(random_bytes(32));
```

### Token létrehozása

Amikor egy felhasználó sikeresen bejelentkezik, generáljunk egy PASETO tokent:

```php
use ParagonIE\Paseto\Builder;
use ParagonIE\Paseto\Purpose;
use ParagonIE\Paseto\Protocol\Version4;

$token = Builder::getLocal($secretKey, new Version4());
$token
    ->setIssuedAt()
    ->setNotBefore()
    ->setExpiration(new \DateTime('+1 hour'))
    ->setSubject($user->id)
    ->setClaims([
        'email' => $user->email,
        'role' => $user->role
    ]);

$tokenString = $token->toString();
```

### Middleware létrehozása

Hozzunk létre egy middleware-t a tokenek ellenőrzésére:

```php
use ParagonIE\Paseto\Parser;
use ParagonIE\Paseto\Purpose;
use ParagonIE\Paseto\Rules\IssuedBy;
use ParagonIE\Paseto\Rules\NotExpired;

class PasetoAuthMiddleware
{
    public function handle($request, Closure $next)
    {
        $tokenString = $request->bearerToken();
        
        if (!$tokenString) {
            return response()->json(['error' => 'Unauthorized'], 401);
        }

        try {
            $parser = Parser::getLocal($secretKey, new Version4());
            $parser
                ->addRule(new NotExpired)
                ->setPurpose(Purpose::local());

            $token = $parser->parse($tokenString);
            
            // Token érvényes, beállítjuk a felhasználót
            $request->user = User::find($token->getSubject());
            
            return $next($request);
        } catch (\Exception $e) {
            return response()->json(['error' => 'Invalid token'], 401);
        }
    }
}
```

### Útvonalak védelme

Végül, alkalmazzuk a middleware-t az API útvonalra:

```php
Route::middleware('paseto.auth')->group(function () {
    Route::get('/protected-route', 'ProtectedController@index');
});
```