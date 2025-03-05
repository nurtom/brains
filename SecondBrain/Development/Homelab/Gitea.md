## docker-compose.yml

```yml
networks:
	gitea:
		external: false

services:
	server:
		image: docker.io/gitea/gitea:latest
		container_name: gitea
		environment:
			- USER_UID=1026
			- USER_GID=100
		restart: always
		networks:
			- gitea
		volumes:
			- ./data:/data
			- /etc/TZ:/etc/TZ:ro
			- /etc/localtime:/etc/localtime:ro
		ports:
			- "9905:3000"
			- "2222:22"
```