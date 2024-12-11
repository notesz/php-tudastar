# OWASP

Az OWASP (Open Web Application Security Project) egy nemzetközi non-profit szervezet, amely a szoftverek és webalkalmazások biztonságának fejlesztésén dolgozik és ingyenesen elérhető útmutatókat és segédanyagokat biztosít fejlesztőknek.

Weboldaluk: [owasp.org](https://owasp.org)
Elérhető dokumentációk: [github.com/OWASP/ASVS](https://github.com/OWASP/ASVS)

## Az OWASP által meghatározott 10 legkritikusabb biztonsági kockázat

Ez a lista segít a fejlesztőknek és biztonsági szakembereknek azonosítani és kezelni a legkritikusabb biztonsági kockázatokat a webalkalmazásokban. Fontos megjegyezni, hogy bár ez a lista 2024-ben is érvényes, az OWASP rendszeresen frissíti a Top 10 listát az aktuális fenyegetések és trendek alapján.

1. **Broken Access Control (Törött hozzáférés-vezérlés)**: Ez a sérülékenység lehetővé teszi a támadók számára, hogy jogosulatlanul férjenek hozzá erőforrásokhoz vagy funkciókhoz.

2. **Cryptographic Failures (Kriptográfiai hibák)**: Olyan problémák, amelyek az érzékeny adatok nem megfelelő titkosításából vagy védelméből erednek.

3. **Injection (Injekció)**: Ide tartoznak az SQL injection, NoSQL injection és más hasonló támadások, amelyek során a támadó rosszindulatú kódot juttat be a rendszerbe.

4. **Insecure Design (Nem biztonságos tervezés)**: Ez a kategória a tervezési és architekturális hibákra összpontosít, amelyek már a fejlesztés korai szakaszában bekerülnek a rendszerbe.

5. **Security Misconfiguration (Biztonsági félrekonfigurálás)**: Ide tartoznak a nem megfelelően beállított biztonsági beállítások, alapértelmezett konfigurációk és hasonló problémák.

6. **Vulnerable and Outdated Components (Sebezhető és elavult komponensek)**: Ez a pont a nem naprakész vagy ismert sérülékenységekkel rendelkező szoftverkomponensek használatára hívja fel a figyelmet.

7. **Identification and Authentication Failures (Azonosítási és hitelesítési hibák)**: Olyan problémák, amelyek a felhasználók azonosításával és hitelesítésével kapcsolatosak.

8. **Software and Data Integrity Failures (Szoftver- és adatintegritási hibák)**: Ez a kategória az adatok és szoftverek integritásának megőrzésével kapcsolatos kockázatokra fókuszál.

9. **Security Logging and Monitoring Failures (Biztonsági naplózás és monitorozás hibái)**: A nem megfelelő vagy hiányos naplózás és monitorozás, amely megnehezíti a biztonsági incidensek észlelését és kezelését.

10. **Server-Side Request Forgery (SSRF) (Szerver oldali kérés hamisítás)**: Olyan támadások, amelyek során a támadó a célszerver nevében küld kéréseket más rendszereknek.