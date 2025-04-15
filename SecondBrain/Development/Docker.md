## run a command as root

for executing commands as root in a running container which uses another user (e.g. node)

```bash
docker container exec -u 0 -it <container_name> bash
```

or 

```bash
docker exec -it eb0a6adb1391 bash
```

## Make the container reachable to an external client

Port Bindings can be include the IP of the Host-Machine, e.g. in docker-compose.yml:

```yml
ports:
	- 10.9.79.35:3003:3003
```

## update stack running via docker compose 

```bash
docker-compose pull
docker-compose up --force-recreate --build -d
docker image prune -f
```