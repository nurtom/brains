Create portainer data volume
```bash
docker volume create portainer_data
```

Run portainer container
```bash
 docker run -d -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:lts
```

or as `docker-compose.yml`

```yml
networks:
  npm:
    name: npm
    external: true

services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
#    ports:
#      - 9000:9000
    environment:
      - VIRTUAL_HOST=portainer.nurtom.duckdns.org
    volumes:
      - portainer_data:/data
      - /var/run/docker.sock:/var/run/docker.sock
    restart: unless-stopped
    networks:
      - npm
volumes:
  portainer_data:
```

## Connect Synology environment to a portainer instance

https://www.reddit.com/r/synology/comments/o9q95c/connect_portainer_to_docker_on_synology_using_the/