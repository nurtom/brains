## run a command as root

for executing commands as root in a running container which uses another user (e.g. node)

```bash
docker container exec -u 0 -it <container_name> bash
```

or 

```bash
docker exec -it eb0a6adb1391 bash
```