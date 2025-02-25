Create portainer data volume
```bash
docker volume create portainer_data
```

Run portainer container
```bash
 docker run -d -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:lts
```

