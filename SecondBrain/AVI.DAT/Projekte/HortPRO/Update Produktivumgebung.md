## Hort Manager

SSH Richtung Server (root)

- auf allen Server (beta-web1, beta-web2)

Manager -> manuell (git bare, push)

- git remote müssen eingerichtet sein

```bash
hort-beta-web1  ssh://service@192.168.7.111:22/home/service/hortpro-manager.git (fetch)
hort-beta-web1  ssh://service@192.168.7.111:22/home/service/hortpro-manager.git (push)
hort-beta-web2  ssh://service@192.168.7.112:22/home/service/hortpro-manager.git (fetch)
hort-beta-web2  ssh://service@192.168.7.112:22/home/service/hortpro-manager.git (push)
hort-dev-web1   ssh://service@192.168.7.114:22/home/service/hortpro-manager.git (fetch)
hort-dev-web1   ssh://service@192.168.7.114:22/home/service/hortpro-manager.git (push)
hort-dev-web2   ssh://service@192.168.7.115:22/home/service/hortpro-manager.git (fetch)
hort-dev-web2   ssh://service@192.168.7.115:22/home/service/hortpro-manager.git (push)
hort-prod-web1  ssh://service@192.168.7.101:22/home/service/hortpro-manager.git (fetch)
hort-prod-web1  ssh://service@192.168.7.101:22/home/service/hortpro-manager.git (push)
hort-prod-web2  ssh://service@192.168.7.102:22/home/service/hortpro-manager.git (fetch)
hort-prod-web2  ssh://service@192.168.7.102:22/home/service/hortpro-manager.git (push)
hort-prod-web3  ssh://service@192.168.7.103:22/home/service/hortpro-manager.git (fetch)
hort-prod-web3  ssh://service@192.168.7.103:22/home/service/hortpro-manager.git (push)
```

dev deployed per git hook automatisch für branch develop!, sonst nichts automatisch

- erst check Versionen im gitlab graph
https://dwh-git.avi-dat.de/hortpro/hort-manager/-/network/develop?ref_type=heads
check ob alles gepusht ist

erst abhängige module, dann Manager aktualiseren
1. Manager hochladen: git push hort-beta-web1/2 develop master 1.25.2
2. mobil: Gitlab Pipelines -> trigger beta
3. extensions: Gitlab Pipelines > trigger beta
4 evtl.: Holidays (muss noch auf Pipeline umgestellt werden)

prepare Manager (ssh auf allen server)
 /var/hortpro/environment/hortpro-manager/deploy/prepare/hortpro-manager-prepare.sh -?

 /var/hortpro/environment/hortpro-manager/deploy/prepare/hortpro-manager-prepare.sh -b develop

update:
/var/hortpro/environment/hortpro-manager/deploy/update/batch-update-vhosts.sh -y -d

check via system-check.php
## Elternportal

gitlab-> trigger beta (macht ein prepare)
einaloggen auf z.B. https://elternportal-beta.hortpro.de/

elternportal -> Pipeline

mobile -> Pipeline
## update prod

- während Batch update sollten alle hintergrundprozesse aus sein
- falls doch was läuft werden Cache Dateien und /var/vhost… abgelegt (doctrine templates, Volt templates, etc.)

-> dann im /var/hortpro/Environment/hortpro-Manager/scripts/vhost-clearcache aufrufen!
-> Nehmen wir in die batch-update-vhosts mit aus


