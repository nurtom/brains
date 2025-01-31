- 2025/01/20
- mit Sebastian und Quentin via Teams

>Apns.avi-dat.de Webserver für die Rufbereitschafts App, von dort werden auch die Push-Nachrichten verschickt (Linux, Apache etc,) Siehe: https://dokuwiki.avi-dat.de/doku.php?id=itmedia:apns
## Datenquellen

 - E-Mails kommen rein: Roundcube -> Roundcube (unser E-Mail) pusht uns die Sachen an unseren Server per Post-Request (Steffen managed Regeln welche Mails überstellt werden, basierend auf Header in den Mails) ->
	 - Weiterleitung über ein /etc script auf dem Mailserver (siehe Ordern roundcube-import)
	 - Früher war das nicht über post-Request, sondern direktes sql insert
	 - Roundcube import-script /etc/aliases
 - Zweite Schnittstelle: Projektmanager für Zugriff auf die Rufbereitschaftszeiten (kommen über sql sync rein nach t_watch_intervals ist ein view) -> kommen eigentlich über die oecd datenbank on_call_duty (siehe avidat.itm/projectmanager.sync/sync.sh) wird über crontab rein (crontab -l) die config dafür kommt aus ~/conf/avidat.itm/projectmanager.sync (hat Kay G. bereitgestellt -> bei Fragen)
## Push Notifications

 - Push-Notifications: siehe scripte ~/betrieb-cron/*
 - Lief früher über jährlich auszutauschende Zertifikate, ist jetzt aber stabil
 - Alte oecd app: 2012 mit objective c etnwickelt, micha z hatte schon swift migration angefangen, war dann aber weg ohne abschluss und übergabe
 - Alte App war eine Art e-mail client, daher musste man die Mails als gelesen markieren weil es sonst nach 15 Minuten immer wieder gebimmelt hat -> neue App erkennt wierholungen (via Fingerprinter.php im Code)
 - Mitteileungen hat jeder bekommen (auch Leute die keine RF hatten), das heisst jeder musst auch den gelesen status managen
 - Aktuelle App können jetzt mehrerer Leute RF haben und auch für unterschiedliche Themen -> ist vor Weihnachten live gegangen aber auch noch nicht ganz fertig. Achtung: Erinnerung an ungelesene Mails muss aktuell noch fertig gestellt werden (entweder Sebastian schaffts noch oder er legt einen Feature Branch an)
 - Alte app war native ios app, die aktuelle ist nur eine auf webview basierende
 - Alte app hatte sich den state lokal synchronisert, der ist aber regelmäßig auseinandergelaufen  und die app musste neu gesynct werden
 - Alte Infrastruktur zum Herunterladen der App kann weg (war notwendig da alte App als Enterprise App selbst gehostet werden musste), die neue App kann global jeder runter laden wenn er die konkrete uri vom Webstore kennt.
 - Aktuelle app wurde 2022 in den Store geladen, im Grunde ist die App nur ein Template mit Hilfsbibliothek (turbo-native) was Sebastian übernommen hat und nur die URL übernommen hat. Aktuell unwahrscheinlich dass sich da was ändert.
- Todo: Weiterleitung Apple developer account Kommunikation einrichten (Mich hinterlegen in er Organisation (Mike oder Danny))
- Rf wird im Projektmanager gepflegt (t_watch_intervals_other sind die neuen Rufbereitschaften ID Now, DG, alles andere außer DAMA) Werden von Kay oder ilja eingepflegt
- T_watch_interval ist view als union auf t-watch_intervall_other und on_call_duty
- Rufbereitschaften werden monatlich kurz vor Monatsende eingepflegt
## Deployment

- Deployment: über Archive und symlinks manuell
- Achtung auf apns Berechtigungen: muss vom web und vom cronjob aufrufbar sein, daher muss cache und log von jeden Lesbar/Schreibbar sein.
- Sebasitan legt ein deploymant Script mit den einzelschritten mit ab

>[!warning] Sebastian per Teams am 29.01.2025:
>*Nachtrag: Achtung, beim Deploy ist wichtig, dass ```var/``` für alle User schreibbar ist, da die Cronjobs nicht mit __www-data__ laufen, sondern mit dem __service__-Nutzer. Die Logik dafür habe ich in ```bin/deploy``` hinterlegt. Falls die Rufbereitschaft-Erinnerungen nicht funktionieren (also die Cronjobs), einfach mal auf dem Server direkt ausführen, lag zuletzt an fehlenden Dateirechten.*
## Entwicklung

- DB-Migation wurden nicht genutzt, könnten aber genutzt werden, da die App die alleinige Hoheit über die Datenbankstruktur hat
- App-icons Ordner: Icon Generator, der dynamische Icons erzeugt, da hat sich Sebastian eins raus gesucht
- Entity: devices.push_token ist die Empfängeradresse für Push-Nachrichten (Achtung kann sich ändern, kommt über UserAGentListener) in ios: SceneDelegate:14 wir der generiert
- Push lokal entwicklt: Xcode kann schnell was aufs device pushen, eventuell kann das dann auch mit IP/localhost kommunizieren. Emulator geht nicht, der kann keine push tokens generieren
- Quellen/Views: Zone ist der Zeit-Bereich in dem man grade ist können verschiedene Notifications mit verschiedenen Klingeltönen definiert werden
- Bereitschaften: Zuordnung watch_interval zu view

***
## Software für DB-Zugriff unter MacOS

- Sequel ace

***
## Nachtrag Push-Nachrichten für Entwicklungsumgebung 20250129

- es gibt eine Dev Url für Push: https://developer.apple.com/documentation/usernotifications/sending-notification-requests-to-apns
- sandbox URL, benötigt eventuell ein anderes Keyfile, vielleicht aber auch nicht (alte .p8 Files auf dem Prod-System sind wahrscheinlich von alten Versionen)
- AUf dem Prodserver liegt nich eine Zwischenversion mit alter App und neuem Push unter ```/home/service/betrieb-ios-push```: das kann weg/gelöscht werden
- Wahrscheinlich funktioniert der aktuelle Schlüssel auch für die sandbox und dann hoffentlich auch für compilierte Entwicklungs iOS Versionen