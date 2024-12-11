# Mockok és stubok használata egy TDD folyamatban

A mockok és stubok használata kulcsfontosságú a TDD (Test-Driven Development) folyamatban, különösen amikor külső függőségekkel vagy komplex objektumokkal dolgozunk.

Íme, hogyan használhatjuk ezeket hatékonyan:

## Mockok használata

A mockok olyan objektumok, amelyek szimulálják egy valódi objektum viselkedését, és lehetővé teszik a velük való interakciók ellenőrzését.

### 1. Függőségek izolálása

```php
public function testUserServiceSendsEmail()
{
    $mockMailer = $this->createMock(Mailer::class);
    $mockMailer->expects($this->once())
               ->method('send')
               ->with('user@example.com', 'Welcome!');

    $userService = new UserService($mockMailer);
    $userService->registerUser('user@example.com');
}
```

Ez a teszt ellenőrzi, hogy a `UserService` megfelelően használja-e a `Mailer` objektumot, anélkül, hogy ténylegesen e-mailt küldene.

### 2. Visszatérési értékek meghatározása

```php
public function testUserRetrievalFromDatabase()
{
    $mockDatabase = $this->createMock(Database::class);
    $mockDatabase->method('findUser')
                 ->willReturn(['id' => 1, 'name' => 'John Doe']);

    $userRepository = new UserRepository($mockDatabase);
    $user = $userRepository->getUserById(1);

    $this->assertEquals('John Doe', $user->getName());
}
```

Itt a mock adatbázis egy előre meghatározott eredményt ad vissza, lehetővé téve a `UserRepository` tesztelését valódi adatbázis-kapcsolat nélkül.

## Stubok használata

A stubok egyszerűbb objektumok, amelyek előre meghatározott válaszokat adnak a hívásokra, de nem ellenőrzik a velük való interakciókat.

### 1. Egyszerű válaszok szimulálása

```php
public function testCalculatorUsesExternalApi()
{
    $stubApi = $this->createStub(ExternalApi::class);
    $stubApi->method('getExchangeRate')
            ->willReturn(1.2);

    $calculator = new CurrencyCalculator($stubApi);
    $result = $calculator->convertUsdToEur(100);

    $this->assertEquals(120, $result);
}
```

Ez a teszt egy egyszerű stub-ot használ az `ExternalApi` helyettesítésére, lehetővé téve a `CurrencyCalculator` tesztelését valódi API-hívások nélkül.

### 2. Kivételek szimulálása

```php
public function testHandlingOfApiErrors()
{
    $stubApi = $this->createStub(ExternalApi::class);
    $stubApi->method('getExchangeRate')
            ->willThrowException(new ApiException('Service unavailable'));

    $calculator = new CurrencyCalculator($stubApi);

    $this->expectException(CalculationException::class);
    $calculator->convertUsdToEur(100);
}
```

Itt a stub egy kivételt dob, lehetővé téve a hibakezelés tesztelését.

## TDD folyamat mockok és stubok használatával

1. **Írj egy bukó tesztet:** Kezdd a teszt írásával, amely meghatározza az elvárt viselkedést, használva mockokat vagy stubokat a függőségek helyettesítésére.

2. **Implementáld a kódot:** Írd meg a minimális kódot, amely átmegy a teszten.

3. **Refaktorálj:** Tisztítsd meg a kódot, miközben biztosítod, hogy a tesztek továbbra is átmennek.

4. **Ismételd:** Folytasd a folyamatot további tesztek hozzáadásával, szükség szerint bővítve vagy módosítva a mockokat és stubokat.