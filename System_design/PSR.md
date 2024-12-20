# PSR

A PSR (PHP Standard Recommendation) egy PHP specifikáció, amelyet a PHP Framework Interoperability Group (PHP-FIG) tesz közzé.

A PSR-ek célja a PHP programozási koncepciók szabványosítása.

Hivatalos dokumentáció:

- [PHP Standards Recommendations](https://www.php-fig.org/psr/)

## Főbb jellemzők

- **Szabványosítás**\
A PSR-ek közös technikai alapot biztosítanak a bevált programozási és tesztelési gyakorlatok megvalósításához.

- **Interoperabilitás**\
Lehetővé teszik a különböző komponensek és keretrendszerek közötti együttműködést.

- **Közösségi fejlesztés**\
A PSR-eket a PHP közösség tagjai javasolják és szavazzák meg egy meghatározott protokoll szerint.

## Elfogadott PSR-ek

- **PSR-1**: Basic Coding Standard
- **PSR-3**: Logger Interface
- **PSR-4**: Autoloading Standard
- **PSR-6**: Caching Interface
- **PSR-7**: HTTP Message Interface
- **PSR-11**: Container Interface
- **PSR-12**: Extended Coding Style Guide
- **PSR-13**: Hypermedia Links
- **PSR-14**: Event Dispatcher
- **PSR-15**: HTTP Handlers
- **PSR-16**: Simple Cache
- **PSR-17**: HTTP Factories
- **PSR-18**: HTTP Client
- **PSR-20**: Clock

## PSR megfelelés

A PHP kód PSR (PHP Standard Recommendation) megfelelőségének ellenőrzésére több hatékony eszköz áll rendelkezésre. Íme a leggyakrabban használt megoldások:

### PHP_CodeSniffer

A PHP_CodeSniffer egy széles körben elterjedt eszköz, amely ellenőrzi a kódot előre meghatározott kódolási szabványok (például PSR-12, PSR-2) alapján. Használata:

```bash
./vendor/bin/phpcs --standard=PSR12 src/
```

### PHP CS Fixer

A PHP CS Fixer nemcsak észleli, de automatikusan javítja is a PSR szabványoktól való eltéréseket. Futtatása:

```bash
./vendor/bin/php-cs-fixer fix src/
```

### PHPStan

A PHPStan egy erőteljes statikus elemző eszköz, amely átfogó típusellenőrzést végez és potenciális hibákat tár fel a PHP kódban. Használata:

```bash
./vendor/bin/phpstan analyse src tests
```

### PHPMD (PHP Mess Detector)

A PHPMD azonosítja a potenciális problémákat és "kód szagokat" a PHP kódban, segítve a fejlesztőket a kódbázis tisztításában és refaktorálásában.

### Integrált fejlesztőkörnyezetek

Egyes IDE-k, mint például a PHPStorm, beépített támogatást nyújtanak a PSR szabványok betartásához. Ezek az eszközök gyakran valós időben jelzik a szabványoktól való eltéréseket, és javaslatokat tesznek a javításukra.