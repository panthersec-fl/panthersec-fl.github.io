---
title: Short Homelab History
date: 2024-8-17 4:41:00
categories: [homelab]
tags: [homelab]
---
#### Beginnings

&nbsp;&nbsp;&nbsp;&nbsp;During an internship I was fortunate enough to acquire a Lenovo mini PC that was no longer needed in their production environment. I was quick to jot down all of the VMs I wanted to run, various technologies to implement and security tools to test out. But, because I was just recently an intern in my first IT role, I did not have the slightest clue on how to configure it.   
&nbsp;&nbsp;&nbsp;&nbsp;Queue YouTube tutorials, r/homelab browsing and lurking on various security focused and university Discord channels. Through it all I did decide on a few things, which is still relevant to my homelab today:

- Hypervisor: Proxmox
- Firewall/Router: PfSense
- VPN: OVPN

That last item did come much later though. 

#### Homelab v0.5
Hardware: TP-Link Router, Lenovo Mini\
Running: Proxmox, Windows Server

&nbsp;&nbsp;&nbsp;&nbsp;Did not really use my lab at this point as my student housing internet was very limiting, but it did help me get started with Proxmox and learn how to configure Linux bridges.

#### Homelab v1.0
Hardware: TP-Link Router, Lenovo Mini, TP-Link Switch\
Running: Proxmox, Windows Server, Windows 10 

&nbsp;&nbsp;&nbsp;&nbsp;Now that I had a switch, I could really get creative by hooking up my laptop and desktop but..... still ended up only having Windows machines and didn't really have much time to mess around with it as I was taking difficult classes at UCF at the time. 

#### Homelab v1.5

Need a diagram now...

![image.png](/assets/v1.5.png)

&nbsp;&nbsp;&nbsp;&nbsp;This is where I really started to experiment and make use of the spare hardware I had sitting around. Nothing came overnight and not every container/VM stayed. 
Getting OVPN, Nextcloud, and Security Onion operational was huge for me and my confidence. I probably get the most use out of Nextcloud, which is an amazing self-hosted version of Office for the uninitiated. 
Still working out my solution for notifications and automating patch management. Looks like [Watchtower](https://github.com/containrrr/watchtower) and [AutomaticSecurityUpdates](https://help.ubuntu.com/community/AutomaticSecurityUpdates) are going to be the winners. 

#### Homelab v2 (Current)

![image (2).png](/assets/v2.png)

Major rework of the lab here.

- Migrated PfSense and Security Onion to the SuperMicro as it was better suited for the role. 
- Changed networking slightly to eliminate total network count down to 4.
- Currently experimenting with Keycloak and finding a backup solution for my containers. 
- Rolled out Wazuh to provide myself with an XDR and endpoint vulnerability monitoring.

This is just a quick summary to show the world what I've been working on. My specific configurations and experimentations are to be documented and explained in future blogs. Reach out to me on LinkedIn to share any questions or concerns. :) 
