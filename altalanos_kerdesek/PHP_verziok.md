# PHP verziók

| Főverzió | Alverzió | Release dátum |
| - | - | - |
| 1 | 1.0.0 | 1995.06.08 |
| 2 | 2.0.0 | 1997.11.01 |
| 3 | 3.0.0 | 1998.06.06 |
| 4 | 4.0.0 | 2000.05.22 |
| 5 | 5.0.0 | 2004.07.13 |
| 7 | 7.0.0 | 2015.12.03 |
| 8 | 8.0   | 2020.11.26 |

## Fontosabb PHP verziók

### A PHP 1

Eredeti nevén PHP Tools (Personal Home Page Tools). A „PHP” név első használata.

### A PHP 5 verzió és fontosabb verziói

| Verzió | Megjegyzés |
| - | - |
| 5.0.0 | Megjelenik a Zend Engine II, teljesen új objektumorientált lehetőségekkel |
| 5.1.0 | Új PHP engine, hatékonyságjavítás új fordítói változók bevezetésével. Új interfész adatbázisokhoz. |
| 5.2.0 | A "filter" kiterjesztés alapértelmezett módon elérhető. Natív JSON támogatás. |
| 5.2.17 | Kritikus hibajavítás a lebegőpontos számításokkal kapcsolatosan. |
| 5.3.0 | Namespace támogatás, sqlite3 |
| 5.4.0 | `register_globals`, `safe_mode`, `allow_call_time_pass_reference`, `session_register()`, `session_unregister()` és `session_is_registered()` eltávolítása |
| 5.6.0 | Constant expressions, Variable-length argument lists, Exponentiation using the ** operator, Function and constant importing, phpdbg, php://input. [Bővebben](https://www.php.net/archive/2014.php#id2014-08-28-1) |

### A PHP 7 verzió és fontosabb verziói

| Verzió | Megjegyzés |
| - | - |
| 7.0.0 | Teljesítmény, Uniform Variable Syntax, új operátorok, szigorúbb típusellenőrzés, elavult elemek eltávolítása. [Bővebben](https://www.php.net/ChangeLog-7.php#7.0.0) |
| 7.1.0 | Nullable types bevezetése, visszatérési érték típus megadás, osztály konstansok láthatósága. [Bővebben](https://www.php.net/ChangeLog-7.php#7.1.0) |
| 7.2.0 | Argon2, `ftp_append()`, `hash_hmac_algos()`, `imagesetclip()` [Bővebben](https://www.php.net/ChangeLog-7.php#7.2.0) |
| 7.3.0 | 31%-kal gyorsabb, mint a PHP 7.0, `s_countable()`, `array_key_first()`, `array_key_last()`, Argon2id [Bővebben](https://www.php.net/ChangeLog-7.php#7.3.0) |

### A PHP 8 verzió és fontosabb verziói

| Verzió | Megjegyzés |
| - | - |
| 8.0 | JIT, union és mixed típus, named arguments, attributes, nullsafe operátor (?->), match, `str_contains()`, `str_starts_with()`, `str_ends_with()` [Bővebben](https://www.php.net/ChangeLog-8.php) |
| 8.1 | Enums, Fibers, intersection típusok, never visszatérés [Bővebben](https://www.php.net/ChangeLog-8.php) |
| 8.2 | readonly osztályok, DNF típusok, `ini_parse_quantity()`, `mysqli_execute_query()` [Bővebben](https://www.php.net/ChangeLog-8.php) |
| 8.3 | Típusos osztálykonstansok, `json_validate()`, `mb_str_pad()` [Bővebben](https://www.php.net/ChangeLog-8.php) |
| 8.4 | Property Hooks, új tömb függvények, új multibyte-os string függvények, property hooks [Bővebben](https://www.php.net/ChangeLog-8.php) | 

## Érdekességek

### Hova lett a PHP6?

A PHP6 fejlesztése elkezdődött ugyan, de soha nem került kiadásra. 2010 márciusában hivatalosan is felhagytak vele.

Ennek több oka is volt:

1. **Unicode támogatás**: A PHP6 fő célja a natív Unicode támogatás bevezetése volt, ami jelentős változásokat igényelt volna a nyelv belső működésében. Ez azonban komoly kihívásokat okozott:

   - A UTF-16 használata megnövelte volna a memóriahasználatot és a CPU-terhelést.
   - Teljesítményproblémák léptek fel a Unicode konverziók miatt.

2. **Fejlesztői erőforrások hiánya**: Nem volt elég fejlesztő, aki értette volna a szükséges változtatásokat.

3. **Lassú fejlesztés**: A Unicode problémák miatt a fejlesztés lelassult és végül elakadt.

A PHP6-ba tervezett funkciók egy része végül a PHP 5.3-as és 5.4-es verziókba került beépítésre. A következő fő verzió a PHP7 lett, hogy elkerüljék a zavart a soha meg nem jelent PHP6-tal kapcsolatban.

### HHVM

A Facebook fejlesztette ki a PHP futtatására a HHVM (HipHop Virtual Machine) nyílt forráskódú virtuális gépet.

Hivatalos oldal: [HHVM](https://hhvm.com)

Fő jellemzői:

- Just-in-time (JIT) fordítást használ a kód futtatásához, ami jelentősen növeli a teljesítményt a hagyományos PHP értelmezőkhöz képest.

- A PHP kódot először egy köztes bytecode-ra (HHBC) fordítja, majd ezt alakítja át x86-64 gépi kódra futásidőben.

- Támogatja a Hack programozási nyelvet, amely a PHP egy továbbfejlesztett változata statikus típusokkal.

- Jelentős teljesítménynövekedést és erőforrás-hatékonyságot biztosít a PHP alkalmazásoknak. A Facebook szerint akár 2,5-szeres gyorsulás és 50%-os CPU-használat csökkenés is elérhető vele.

- Kompatibilis a legtöbb PHP kóddal és keretrendszerrel, bár vannak kisebb eltérések.

- Beépített profilozó és hibakereső eszközöket tartalmaz.

A HHVM célja, hogy egyesítse a dinamikus nyelvek rugalmasságát a statikusan fordított nyelvek teljesítményével, így téve hatékonyabbá a nagy PHP alkalmazások futtatását.