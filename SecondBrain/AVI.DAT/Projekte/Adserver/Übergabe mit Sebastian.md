## Migration auf PHP 8.3

- Sebastian macht die aktuelle Migration noch fertig
- Propel wird ausgebaut, nur noch native SQL API, dann für jeden funktionalen Cluster ein ```api_entity/clusert.php```
- In den Controllern wird dann die api per namespace aufgerufen
- Symfony 1 war noch komplett ohne namespaces, früher alles über statische Klassenmethoden
- call_user_array_func war notwendig um Funktionen als Parameter zu übergeben und dynamisch auszuführen

## Neues Feld hinzufügen

- Siehe Video Übergabe ab Minute ca. 25

## Tests

- test/functional/frontend geht noch
	- ```./symfony test:functional frontend``` sollten alle Tests auf grün bleiben außer einer der click-11Test
- test/functional/backend gehen aktuell nicht, sollten dann nach Sebastians Migration wieder gehen
- test/unit ist nicht mehr aktuell und schlägt nach Sebastians Migration fehl (kein Propel mehr)
- apps/jasmine kann weg (hatte Sebastian Kannegießer mal angefangen)
- test/selenium kann weg, weil die nicht mehr funktionieren

## Potentielles Upgrade PHP 9+

- Ab 1h 38m im Video
- Erwartung dass auf github unter FriendsOfSymfony1/symfony1 auch eine Version für die kommenden PHP Updates bereit gestellt wird
- Sonst nur PHP Syntax als PHP Release Migrations Guide ableiten was zwingend zu ändern ist
- Vorgehen: dependencies updaten, Code anpassen, functional tests durchlaufen lassen

## Infrastruktur

- ca. 1h 48m im Video