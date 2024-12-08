## Singleton Pattern

Ez a minta biztosítja, hogy egy osztályból csak egyetlen példány létezzen, és globális hozzáférést biztosít ehhez a példányhoz. Gyakran használják olyan esetekben, amikor egy központi vezérlő objektumra van szükség, például konfigurációkezeléshez vagy erőforrás-megosztáshoz.

A Singleton gyakorlati alkalmazása: [[System design/Design Patterns (Tervezési minták)/Singleton]]

## Factory Method Pattern

Ez a minta lehetővé teszi objektumok létrehozását anélkül, hogy meghatároznánk a pontos osztályt. Hasznos, amikor a kódot el szeretnénk választani a konkrét implementációtól, például különböző formátumú jelentések generálásakor.

A Factory Method gyakorlatilag alkalmazása: [[System design/Design Patterns (Tervezési minták)/Factory Method]] 

## Observer Pattern

Ez a minta egy olyan függőségi viszonyt definiál az objektumok között, ahol ha egy objektum állapota megváltozik, az összes függő objektum automatikusan értesül és frissül. Gyakran használják eseményvezérelt alkalmazásokban és felhasználói felületek frissítésére.

Az Observer gyakorlatilag alkalmazása: [[System design/Design Patterns (Tervezési minták)/Observer]] 

## Strategy Pattern

Ez a minta lehetővé teszi algoritmusok dinamikus cseréjét futásidőben. Akkor hasznos, amikor különböző variációi vannak egy algoritmusnak, és ezeket rugalmasan szeretnénk cserélni.

A Strategy gyakorlatilag alkalmazása: [[System design/Design Patterns (Tervezési minták)/Strategy]] 

## Builder Pattern

Ez a minta elválasztja egy komplex objektum felépítését annak reprezentációjától. Különösen hasznos olyan objektumok létrehozásánál, amelyeknek sok opcionális vagy változó része van, például egy testreszabható termék konfigurálásánál.

A Builder gyakorlatilag alkalmazása: [[System design/Design Patterns (Tervezési minták)/Builder]] 

## Adapter Pattern

Ez a minta lehetővé teszi, hogy inkompatibilis interfészekkel rendelkező objektumok együttműködjenek. Gyakran használják meglévő rendszerek integrálásánál vagy külső könyvtárak használatánál.

Az Adapter gyakorlatilag alkalmazása: [[System design/Design Patterns (Tervezési minták)/Adapter]] 

## Model-View-Controller (MVC) Pattern

Bár ez inkább egy architekturális minta, rendkívül elterjedt a webes és mobil alkalmazások fejlesztésében. Szétválasztja az adatkezelést, a megjelenítést és a felhasználói interakciót, ami tisztább, modulárisabb kódot eredményez.

Az MVC gyakorlatilag alkalmazása: [[System design/Design Patterns (Tervezési minták)/MVC]] 