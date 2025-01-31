https://billing.avi-dat.de
## Funktionen

- grundlegende Funktion ist die monatliche Rechnungserstellung
- Nutzer sind: interne Verwaltung (Conny Eilenberger, Petra Friedrich, nur AVI.DAT intern), Nutzer können alles, keine Rollenbeschränkung, eingeloggte Nutzer können andere Nutzer anlegen/verwalten.
## Stack

- technisch relativ einfach, kein CSS oder JS Framework
- kein ORM nur funktionale SQL Api

## Architektur

- komplex, da Datenbasis historisiert ist (valid_from, vaild_to Spalten in den Entities), kann für jede Entity individuell anders sein, daher kein ORM, weil die Abfrage dafür sonst zu aufwendig geworden wären
- Im Dump sind aktuell nur Daten bis April 2023, Zurückschalten nur über die URL manuell

## Deployment

- Administration Webserver: Steffen