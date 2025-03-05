## Intern

### Home Assistant
http://192.168.22.52:8123

### Nginx Proxy Manager
https://npm.nurtom.duckdns.org

###  Portainer
https://portainer.nurtom.duckdns.org

### Synology DSM
https://diskstation.nurtom.duckdns.org

---
## Public

### Wiki.js
https://wiki.nurtom.de

### Actual Budget
https://budget.nurtom.de

### Vaultwarden (keine Live-Daten)
https://vault.nurtom.de
- Hardening notwendig: https://github.com/dani-garcia/vaultwarden/wiki/Hardening-Guide

## Firefly (fin)

```yml
services:
  app:
    image: fireflyiii/core:latest
    hostname: app
    container_name: firefly_iii_core
    restart: always
    volumes:
      - firefly_iii_upload:/var/www/html/storage/upload
    env_file: .env
    networks:
      - firefly_iii
    ports:
      - 9902:8080
    depends_on:
      - db
  db:
    image: mariadb:lts
    hostname: db
    container_name: firefly_iii_db
    restart: always
    env_file: .db.env
    networks:
      - firefly_iii
    volumes:
      - firefly_iii_db:/var/lib/mysql
  cron:
    #
    # To make this work, set STATIC_CRON_TOKEN in your .env file or as an environment variable and replace REPLACEME below
    # The STATIC_CRON_TOKEN must be *exactly* 32 characters long
    #
    image: alpine
    restart: always
    container_name: firefly_iii_cron
    command: sh -c "echo \"0 3 * * * wget -qO- http://app:8080/api/v1/cron/9d50da195d8432e72a946411d78bb39c\" | crontab - && crond -f -L /dev/stdout"
    networks:
      - firefly_iii

volumes:
   firefly_iii_upload:
   firefly_iii_db:

networks:
  firefly_iii:
    driver: bridge

```