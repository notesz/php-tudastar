# Domain-Driven Design (DDD)

A Domain-Driven Design (DDD), magyarul tartományvezérelt vagy tartományalapú tervezés, egy fontos szoftverfejlesztési megközelítés, amely az üzleti domain (tartomány) köré építi a szoftverrendszereket. A DDD lényege, hogy a szoftverfejlesztés középpontjában az üzleti domain álljon, vagyis az a terület vagy problémakör, amelyet a szoftvernek meg kell oldania vagy támogatnia kell.

## A DDD fő elemei és céljai

### Közös nyelv kialakítása

A DDD egyik kulcsfontosságú eleme az úgynevezett "ubiquitous language" (mindenütt jelen lévő nyelv) kialakítása. Ez egy olyan közös nyelvet jelent, amelyet mind a fejlesztők, mind az üzleti szakértők használnak és értenek. Ez a közös nyelv nemcsak a kommunikációban jelenik meg, hanem a kódban is tükröződik, például a változók, metódusok és osztályok elnevezésében.

### Üzleti logika és technológia összehangolása

A DDD célja, hogy a szoftver architektúrája szorosan illeszkedjen az üzleti folyamatokhoz és igényekhez. Ez azt jelenti, hogy a szoftver struktúrája és nyelve (osztálynevek, metódusok, változók) tükrözze az üzleti domaint.

### Komplexitás kezelése

A DDD segít kezelni a komplex üzleti logikát azáltal, hogy a rendszert kisebb, kezelhető egységekre bontja. Ezeket az egységeket "bounded context"-eknek (határolt környezeteknek) nevezzük, amelyek gyakran megfeleltethetők egy-egy mikroszolgáltatásnak.

## A DDD gyakorlati alkalmazása

### Domain modellezés

A DDD központi eleme a domain modell kialakítása, amely a domain kulcsfogalmait, szabályait és folyamatait tartalmazza. Ez a modell szolgál alapul a szoftver tervezéséhez és fejlesztéséhez.

### Építőelemek

A DDD több fontos építőelemet használ, mint például:

- Entitások: egyedi azonosítóval rendelkező objektumok
- Értékobjektumok: azonosító nélküli, értékük által meghatározott objektumok
- Aggregátumok: logikai egységet alkotó objektumcsoportok

### Rétegek

Egy DDD-alapú alkalmazás tipikusan több rétegből áll:

- Domain réteg: az üzleti logikát tartalmazza
- Alkalmazás réteg: koordinálja a feladatokat
- Infrastruktúra réteg: technikai részleteket kezeli

A DDD tehát egy olyan megközelítés, amely segít a fejlesztőknek és az üzleti szakértőknek együttműködni egy olyan szoftver létrehozásában, amely pontosan tükrözi az üzleti igényeket és folyamatokat, miközben rugalmas és könnyen karbantartható marad.

## Eric Evans

Eric Evans a **Domain-Driven Design: Tackling Complexity in the Heart of Software** című könyv szerzője, amely 2003-ban jelent meg az Addison-Wesley kiadónál. Ez a könyv alapozta meg a DDD koncepcióját és módszertanát.

Evans az 1990-es évek elejétől kezdve számos nagyszabású üzleti rendszer fejlesztésén dolgozott, különböző megközelítéseket alkalmazva. Ezek a tapasztalatok szolgáltak alapul a DDD módszertanának kidolgozásához.