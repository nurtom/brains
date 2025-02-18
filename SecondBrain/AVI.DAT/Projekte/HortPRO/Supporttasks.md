## Feature freischalten
#hortmanager

Verfügbare Features sind Verträge, Elternportal, Abstimmungen, Essenplaner, Import/Exporttool. Feature werden auf Domain-Basis freigeschalten. Die Freischaltung muss nur auf einem Server erfolgen, wird in damit in der Datenbank gespeichert und gilt dann auf allen Servern.

```bash
# connect to a production server
ssh service@hort-prod-web1

# switch to domain
cd /var/hortpro/vhosts
cd <domain>

# show current features configuration and availabele feature keys
src/bin/cli -t config -a listFeatures

# enable feature meal planner
src/bin/cli -t config -a enableFeature -p mealPlanner
```

Oder https://domain.hortpro.de/install/system-check.php aufrufen und auf __Open Setup__ Link klicken.

## Datenschutz Betroffenenanfrage Elternportal
#datenschutz

Um unsere Auskunftspflicht nachzukommen, müssen wir ad-hoc beantworten können, ob wir Daten zu einem speziellen Nutzer in unserem System speichern. Üblicherweise bekommen wir Name und Naschrift einer Person dazu.

Mit Elternportal Produktivsystem verbinden
```bash
ssh ep-prod-web1
cd /var/hortpro/elternportal/server
cat .env
# Datenbank credentials copy paste

mysql -h 192.168.7.20 -uelternportal -p
```

>[!warning]
>Das Suchen via ```heptools user:search``` reicht nicht aus, da hier nur die E-Mail Adresse als Suchkriterium genutzt wird!

Datensatz per MySQL finden, z.B. per Nachnamen:
```mysql
USE elternportal;
SELECT * FROM user WHERE lastname LIKE '%Nachname%';
```
