- im VF (53er)
- im Wiki unter Marketing:MDM Ladungsmonitor
- https://ls.m-dwh.de Credentials: admin/lej
- Übersicht über SQL Prozsess oder Perl Skripte, Beladungen mit ihrem Status werden dargestellt
- relativ alt (ca 2005)
- Nutzer sind: Stefan Riemer (nur interne Nutzer)
- Objekte: Kann Tabelle oder ET-Task oder SQL-Skript oder... sein
- Im Gitlab: mdm/control-m-2.x
- ist seit ca 2022 auf PHP 8
- Smarty als templating engine
- SSH Auf Liveserver: Mit KDG-Domainnutzer
- Es gibt Varianten/Kopien vom Frontend:
	- vmk/ls-vmk (deployed als prod, int, test zB. https://vmk-int-ls2.m-dwh.de)
		- Funktional etwas weniger 172.29.20.108
	- d2d-ls (Door2Door ist nochmal eine Kopie vom VMK)
- Deployment
	- Projekte sind direkt auf dem Server ausgecheckt
	- Konfiguration env Variablen über nginx host Config
	- Die Varianten liegen alle auf verschiedenen Servern
	- Ordern für die ausgecheckten Projekte immer individuell über Apache/Nginx config ableiten