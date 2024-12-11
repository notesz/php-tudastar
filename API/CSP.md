# CSP

A Content Security Policy (CSP) egy olyan biztonsági szabvány, amely további védelmi réteget biztosít a webalkalmazások számára. A CSP fő célja bizonyos típusú támadások megelőzése.

## A CSP működése

A CSP egy HTTP válaszfejlécként kerül elküldésre a böngészőnek, amely meghatározza, hogy milyen erőforrásokat tölthet be biztonságosan az adott weboldal. Ezáltal a böngésző korlátozza a betölthető tartalmakat, például:

- JavaScript kódokat
- CSS stíluslapokat
- Képeket

## Főbb jellemzők

- A CSP lehetővé teszi a weboldal tulajdonosának, hogy pontosan meghatározza, mely forrásokból származó tartalmak tölthetők be.
- Alapértelmezetten blokkolja az inline szkripteket és a `eval()` függvény használatát.

## Példa a CSP beállítására

A Content Security Policy (CSP) beállítása egy weboldalon több lépésből áll:

### 1. HTTP fejléc beállítása

Először érdemes a CSP-t jelentési módban beállítani a `Content-Security-Policy-Report-Only` HTTP fejléccel. Ez lehetővé teszi a policy finomhangolását anélkül, hogy blokkolná a tartalmat.

### 2. CSP szabály létrehozása

A megbízható források azonosítása után állítsa össze a `Content-Security-Policy` HTTP fejlécet. Például:

```
Content-Security-Policy: default-src 'self' *.adobe.com
```

### 3. Implementálja a CSP-t

A CSP-t kétféleképpen lehet implementálni:

1. HTTP fejlécként:
```
Content-Security-Policy: default-src 'self' *.adobe.com
```

2. HTML meta tagként:
```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self' 'unsafe-inline' 'unsafe-eval' *.cloudfront.net">
```

### 4. Finomhangolás

Használjon specifikus direktívákat az erőforrások típusainak pontosabb szabályozásához. Például:

```
Content-Security-Policy: script-src *.google.com *.adroll.com
```

### 5. Tesztelje a CSP-t

Mielőtt élesben alkalmazná, tesztelje a CSP-t, hogy megbizonyosodjon arról, nem blokkol-e szükséges erőforrásokat. Használhatja a `Content-Security-Policy-Report-Only` fejlécet és a `report-uri` direktívát a szabálysértések naplózásához.