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
