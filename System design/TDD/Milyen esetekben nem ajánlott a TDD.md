# Milyen esetekben nem ajánlott a TDD

A Tesztvezérelt Fejlesztés (TDD) általában hasznos módszer, de vannak esetek, amikor nem ajánlott vagy kevésbé hatékony. Íme néhány helyzet, amikor érdemes megfontolni a TDD mellőzését:

## Bizonytalan követelmények esetén

Ha nem világos, pontosan mit kell megvalósítani, a TDD nem feltétlenül segít. Ilyenkor jobb lehet először egy működő megoldást kidolgozni, és csak utána írni hozzá teszteket.

## Gyors prototípusok készítésekor

Egyszer használatos kódok vagy gyors prototípusok esetén a TDD túlzott erőfeszítést jelenthet[2]. Az ilyen "eldobható" kódoknál nem feltétlenül szükséges a szigorú tesztelés.

## Meglévő, teszteletlen kódbázis esetén

Ha egy régi, tesztek nélküli rendszert kell módosítani, nehéz lehet azonnal TDD-t alkalmazni[3]. Ilyenkor érdemes először néhány tesztet írni a meglévő funkcionalitásra, mielőtt új fejlesztésbe kezdünk.

## Egyszerű CRUD műveleteknél

Az egyszerű adatbázis műveleteknél (létrehozás, olvasás, frissítés, törlés) nem mindig szükséges a TDD[3]. Ezeket érdemes inkább izolálni és a repository mintát alkalmazni.

## Időkritikus projekteknél

A TDD extra időt és erőfeszítést igényel a fejlesztés elején[4]. Ha nagyon szoros a határidő, ez problémát okozhat, bár hosszú távon általában megtérül a befektetett idő.

## Amikor a csapat nem egységes

Ha a fejlesztőcsapat nem minden tagja alkalmazza a TDD-t, az problémákat okozhat[5]. A TDD befolyásolja a kód tervezését, ezért fontos, hogy a csapat egységesen használja vagy mellőzze.

Fontos megjegyezni, hogy még ha nem is alkalmazzuk szigorúan a TDD-t, az automatizált tesztek írása általában hasznos és ajánlott gyakorlat a szoftverfejlesztésben.