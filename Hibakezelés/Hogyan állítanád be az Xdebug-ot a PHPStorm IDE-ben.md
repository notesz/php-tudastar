# Hogyan állítanád be az Xdebug-ot a PHPStorm IDE-ben

Az Xdebug beállítása PHPStorm IDE-hez a következő lépéseket foglalja magában:

1. Xdebug telepítése:

   - Linux/Unix/macOS rendszereken használhatod a PECL-t: `pecl install xdebug`
   - Windows esetén töltsd le a megfelelő DLL fájlt az Xdebug weboldaláról, és helyezd el a PHP kiterjesztések könyvtárában.

2. PHP konfigurálása az Xdebug használatához:

   - Keresd meg a php.ini fájlt: `php --ini`
   - Szerkeszd a php.ini fájlt, és add hozzá a következő sorokat:

```ini
     zend_extension="/path/to/your/xdebug.so"
     xdebug.mode=debug
     xdebug.start_with_request=yes
     xdebug.client_port=9003
```

3. Apache újraindítása (ha használod):\
   `sudo service apache2 restart`

4. PHPStorm konfigurálása:

   - Nyisd meg a Beállításokat (Settings)
   - Navigálj a Languages & Frameworks &gt; PHP &gt; Debug menüponthoz
   - Ellenőrizd, hogy az Xdebug port 9003-ra van állítva
   - A PHP &gt; Servers menüpontban állíts be egy új szervert a projektedhez

5. Debugolás indítása:

   - Állíts be töréspontokat a kódban
   - Kattints a "Start listening for PHP Debug Connections" gombra a PHPStorm eszköztáron
   - Indítsd el az alkalmazásodat, és a PHPStorm meg fog állni a töréspontoknál

Ezekkel a lépésekkel beállíthatod az Xdebug-ot a PHPStorm IDE-ben, ami lehetővé teszi a hatékony PHP debugolást.

További részletek:\
<https://www.jetbrains.com/help/phpstorm/debugging-with-phpstorm-ultimate-guide.html>