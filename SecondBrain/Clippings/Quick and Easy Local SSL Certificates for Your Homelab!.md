---
title: "Quick and Easy Local SSL Certificates for Your Homelab!"
source: "https://www.youtube.com/watch?v=qlcVx-k-02E&t=20s"
author:
  - "[[Wolfgang's Channel]]"
published: 2023-05-15
created: 2025-02-27
description: "To try everything Brilliant has to offer—free—for a full 30 days, visit http://brilliant.org/Wolfgang/ The first 200 of you will get 20% off Brilliant’s annual premium subscriptionFollow me:Mastod"
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=qlcVx-k-02E)  

> [!error]
> For anyone using a fritzbox router: You have to add your full domain as an exception to the "DNS rebind protection", because the fritzbox does not allow DNS resolution of domain names that point to private ips to protect against DNS rebinding attacks

Timestamps:  
00:00 Intro  
00:57 How does it work?  
01:34 Brilliant.org  
02:28 What will we need?  
04:40 Installing Docker – Tutorial starts here  
06:03 docker-compose Walkthrough  
06:46 Generating the certificate  
08:32 Setting up domains  
11:02 Outro

### Gist
1. Domain bei duckdns.org hinzufügen und auf eine IP im privaten Netz (Diskstation) zeigen lassen
2. Eine Ausnahme unter DNS-Rebind Schutz in den Netzwerkeinstellungen der Fritzbox für die neue/eigene duckdns Domain hinzufügen
3. Die Diskstation bindet Port 80 und 443 default, braucht das auch für Dienste wie SynologyDrive etc. Daher ist es sinnvoll eine separate VM im Virtual Machine Manager anzulegen (Ubuntu Server), darauf Docker zu installieren und dann darauf Nginx Proxy Manger auszuführen
4. Die IP im Duck DNS muss dann auf die IP der VM zeigen!
5. 