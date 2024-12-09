Az API throttling egy olyan technika, amely szabályozza az API-khoz érkező kérések számát és sebességét. A throttling fő célja az API-k teljesítményének és stabilitásának megőrzése, valamint a méltányos erőforrás-elosztás biztosítása a felhasználók között.
## A Throttling működése

- Ideiglenesen blokkolja azokat a klienseket, amelyek túllépik az engedélyezett kérési rátát.
- Korlátozza a kérések számát egy meghatározott időintervallumon belül.
- Különböző módszerekkel implementálható, például:
	- Kérések queue-ba állítása
	- Párhuzamos kérések korlátozása
	- Sávszélesség-korlátozás

## A Throttling előnyei

1. Teljesítmény és stabilitás: Megakadályozza a szerver túlterhelését és biztosítja a konzisztens válaszidőket.
2. Méltányos erőforrás-elosztás: Egyenlő hozzáférést biztosít minden felhasználó számára.
3. Skálázhatóság: Segít a kiszámítható terhelés kezelésében.
4. Biztonság: Védelmet nyújt a túlterheléses (DDoS) támadások ellen.
5. Felelősségteljes használat ösztönzése: A fejlesztőket hatékonyabb kódolásra ösztönzi.

## Rate Limiting

A Rate Limiting hasonló, mint a Throttling. Kevésbé agresszívebb módszer, mint a Throttling.

1. Inkább lelassítja a kéréseket, de nem állítja le teljesen.
2. Általában hosszabb időintervallumokra vonatkozik (pl. óra, nap, hónap).
3. Célja a hosszú távú erőforrás-használat szabályozása és a méltányos elosztás biztosítása.
4. Típusai:
	1. Felhasználói szintű korlátozás
	2. Földrajzi alapú korlátozás
	3. Szerver szintű korlátozás