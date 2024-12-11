# Milyen Design Patternek léteznek

A design pattern (tervezési minta) egy általános, újrafelhasználható megoldás gyakran előforduló problémákra a szoftverfejlesztésben. A design pattern-eket három fő kategóriába sorolják a céljuk és a megoldandó problémák alapján:

## 1. Creational Patterns (Létrehozási minták)

Ezek a minták az objektumok létrehozásának folyamatára összpontosítanak. Céljuk, hogy rugalmas és független mechanizmusokat biztosítsanak az objektumok létrehozásához, így csökkentve a rendszer architektúrájára gyakorolt hatást.

### Példák:

- **Singleton**: Biztosítja, hogy egy osztályból csak egy példány létezzen, és globális hozzáférést biztosít ehhez az példányhoz.
- **Factory Method**: Lehetővé teszi az alosztályok példányosítását anélkül, hogy a kliens tudna az osztály konkrét típusáról.
- **Abstract Factory**: Családok létrehozására szolgál, amely különböző típusú objektumokat hoz létre.
- **Builder**: Az objektumok összetett felépítését segíti elő, elválasztva az építési folyamatot a végső reprezentációtól.
- **Prototype**: Lehetővé teszi új objektumok létrehozását meglévő objektumok másolásával.

## 2. Structural Patterns (Szerkezeti minták)

Ezek a minták az osztályok és objektumok összekapcsolásával foglalkoznak, hogy nagyobb struktúrákat alkossanak. Céljuk, hogy leírják, hogyan lehet osztályokat és objektumokat kombinálni új struktúrák létrehozása érdekében.

### Példák:

- **Adapter**: Lehetővé teszi, hogy két inkompatibilis interfész együttműködjön.
- **Bridge**: Elválasztja az interfészt a megvalósítástól, lehetővé téve mindkettő független fejlődését.
- **Composite**: Lehetővé teszi, hogy egyetlen interfészen keresztül kezeljünk egyszerű és összetett objektumokat.
- **Decorator**: Dinamikusan bővíti egy objektum funkcionalitását anélkül, hogy megváltoztatná annak struktúráját.
- **Facade**: Egyszerűsíti a rendszer komplexitását egy egyszerűsített interfész biztosításával.

## 3. Behavioral Patterns (Viselkedési minták)

Ezek a minták az objektumok közötti kommunikációval és felelősségmegosztással foglalkoznak. Céljuk az objektumok közötti együttműködés és koordináció javítása.

### Példák:

- **Observer**: Lehetővé teszi, hogy egy objektum értesítse a hozzá kapcsolódó objektumokat a változásokról.
- **Strategy**: Lehetővé teszi különböző algoritmusok dinamikus kiválasztását futásidőben.
- **Command**: Az utasításokat encapsulálja, lehetővé téve azok késleltetett végrehajtását vagy visszavonását.
- **Chain of Responsibility**: Lehetővé teszi, hogy több objektum kezelje a kéréseket anélkül, hogy tudnának egymásról.

## Összegzés

A design pattern-ek segítenek a szoftverfejlesztőknek olyan bevált megoldások alkalmazásában, amelyek javítják a kód olvashatóságát, karbantarthatóságát és bővíthetőségét. A megfelelő minta kiválasztása segíthet a gyakori problémák hatékony megoldásában.