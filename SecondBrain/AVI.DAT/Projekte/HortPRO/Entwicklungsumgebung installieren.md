im WSL!
## environment installieren

```bash
cd /home/thomas/projects
mkdir horpro && cd hortpro
git clone gitlab@dwh-git.avi-dat.de:hortpro/hortpro-environment.git
cd .\hortpro-environment\develop\docker
chmod u+x init.sh
./init.sh
```

## elternportal/hortpro auschecken

```bash
cd /home/thomas/projects/hortpro
git clone gitlab@dwh-git.avi-dat.de:hortpro/hortpro-eltern-portal.git
git clone gitlab@dwh-git.avi-dat.de:hortpro/hort-manager.git
```

## elternportal einrichten 

https://dwh-git.avi-dat.de/hortpro/hortpro-eltern-portal/-/blob/develop/develop/docker/README.md

```bash
cd hortpro-eltern-portal/develop/docker
chmod u+x init.sh
./init.sh
```


## entwickeln

frontends (hortpro-mobile, hortpro-elternportal/frontend) im wsl aufmachen und "npm run start"