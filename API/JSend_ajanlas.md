# REST API - JSend ajánlás

A JSend egy ajánlás, amely meghatározza hogyan kell strukturálni a REST API válaszait.

Hivatalos oldal: [GitHub](https://github.com/omniti-labs/jsend)

## Fő jellemzők

- **Egyszerűség**: A JSend egy minimális, könnyen érthető formátumot ír elő.
- **Szabványosítás**: Célja, hogy egységesítse a különböző webszolgáltatások JSON válaszainak formátumát.
- **Alkalmazás szintű**: Nem a protokoll vagy átviteli szintre, hanem az alkalmazás szintű üzenetváltásra fókuszál.

## Válasz típusok

1. **Sikeres válasz**:
   - Státusz: "success"
   - Tartalmazza a kért adatokat a `data` kulcs alatt.

Például:

```json
{
    status : "success",
    data : {
        "post" : { 
            "id" : 1, 
            "title" : "A blog post", 
            "body" : "Some useful content" 
        }
     }
}
```

vagy:

```json
{
    status : "success",
    data : null
}
```

2. **Sikertelen válasz**:
   - Státusz: "fail"
   - A `data` kulcs alatt tartalmazza a hiba okát, gyakran validációs hibák formájában.

Például:

```json
{
    "status" : "fail",
    "data" : {
        "title" : "A title is required" 
    }
}
```

3. **Hiba válasz**:
   - Státusz: "error"
   - Tartalmazza a hibaüzenetet és opcionálisan a hibakódot.

Például:

```json
{
    "status" : "error",
    "message" : "Unable to communicate with database"
}
```