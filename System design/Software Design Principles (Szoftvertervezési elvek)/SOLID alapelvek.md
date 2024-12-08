A SOLID elvek alkalmazása egy új projektben segít létrehozni egy jól strukturált, rugalmas és karbantartható kódot. Íme néhány gyakorlati tanács az egyes elvek alkalmazására: #solid 

## Single Responsibility Principle (SRP)

- Tervezd úgy az osztályaidat, hogy minden osztálynak csak egy felelőssége legyen.
- Például, ahelyett hogy egy `User` osztály kezelné a felhasználói adatokat és az adatbázis műveleteket is, hozz létre külön `UserRepository` osztályt az adatbázis műveletekhez.

  #srp 

## Open/Closed Principle (OCP)

- Használj interfészeket és absztrakt osztályokat a viselkedés definiálására.
- Alkalmazz stratégia mintát vagy dekorátor mintát a funkcionalitás bővítéséhez anélkül, hogy módosítanád a meglévő kódot.

  #ocp 

## Liskov Substitution Principle (LSP)

- Tervezd úgy az öröklődési hierarchiádat, hogy az alosztályok valóban helyettesíthetők legyenek a szülőosztályokkal.
- Kerüld az olyan helyzeteket, ahol az alosztály megváltoztatja a szülőosztály viselkedését.

  #lsp 

## Interface Segregation Principle (ISP)

- Hozz létre kisebb, specifikus interfészeket ahelyett, hogy egy nagy, általános interfészt használnál.
- Például egy `Printer` interfész helyett használj külön `Printable` és `Scannable` interfészeket.

  #isp 

## Dependency Inversion Principle (DIP)

- Használj függőség befecskendezést (Dependency Injection) a modulok közötti kapcsolatok lazítására.
- Alkalmazz egy DI konténert a függőségek kezelésére.

  #dip 