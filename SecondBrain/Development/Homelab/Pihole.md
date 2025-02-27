> https://www.smarthomebeginner.com/run-pihole-in-docker-on-ubuntu-with-reverse-proxy/

Make sure Port 53 is not used by systemd-resolved under Ubuntu.

```bash
sudo systemctl disable systemd-resolved.service
sudo systemctl stop systemd-resolved.service
sudo mv /etc/resolv.conf /etc/resolv.conf.bak
```

Configure default dns behavior
```bash
sudo vim /etc/NetworkManager/NetworkManager.conf 
```

Add dns=default line
```bash
[main]
plugins=ifupdown,keyfile
dns=default
```

```bash
sudo service network-manager restart
```

 Start/Stop Pihole
```bash
sudo docker-compose up -d
sudo docker-compose stop
```

