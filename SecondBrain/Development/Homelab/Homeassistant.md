## docker-compose.yml
```yml
services:
	homeassistant:
		container_name: homeassistant
		image: "ghcr.io/home-assistant/home-assistant:stable"
		volumes:
			- ./config:/config
			- /etc/localtime:/etc/localtime:ro
			- /run/dbus:/run/dbus:ro
		restart: unless-stopped
		privileged: true
		network_mode: host
```


## Hardware

Upgrade to Yellow (https://www.home-assistant.io/yellow/)
- POE Yellow https://www.seeedstudio.com/Home-Assistant-Yellow-Kit-with-Power-over-Ethernet-p-5673.html 135 USD
- RPI Compute Module https://www.reichelt.de/de/de/shop/produkt/raspberry_pi_compute_modul_5_8gb_ram_ohne_emmc_wlan-390634 93,05 EUR
- NVME SSD 50 EUR
Setup: https://yellow.home-assistant.io/cm5-kit/