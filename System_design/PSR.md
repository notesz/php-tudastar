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

- **PSR-1**: [Basic Coding Standard](https://www.php-fig.org/psr/psr-1/)
- **PSR-3**: [Logger Interface](https://www.php-fig.org/psr/psr-3/)
- **PSR-4**: [Autoloading Standard](https://www.php-fig.org/psr/psr-4/)
- **PSR-6**: [Caching Interface](https://www.php-fig.org/psr/psr-6/)
- **PSR-7**: [HTTP Message Interface](https://www.php-fig.org/psr/psr-7/)
- **PSR-11**: [Container Interface](https://www.php-fig.org/psr/psr-11/)
- **PSR-12**: [Extended Coding Style Guide](https://www.php-fig.org/psr/psr-12/)
- **PSR-13**: [Hypermedia Links](https://www.php-fig.org/psr/psr-13/)
- **PSR-14**: [Event Dispatcher](https://www.php-fig.org/psr/psr-14/)
- **PSR-15**: [HTTP Handlers](https://www.php-fig.org/psr/psr-15/)
- **PSR-16**: [Simple Cache](https://www.php-fig.org/psr/psr-16/)
- **PSR-17**: [HTTP Factories](https://www.php-fig.org/psr/psr-17/)
- **PSR-18**: [HTTP Client](https://www.php-fig.org/psr/psr-18/)
- **PSR-20**: [Clock](https://www.php-fig.org/psr/psr-20/)

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