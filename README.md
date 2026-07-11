# Unbound recursive DNS resolver with Pi-Hole.
- A Self hosted network wide adblocker backed by a locally run Recursive DNS resolver.
- To core apps used in thisproject are [pi-hole](https://github.com/pi-hole/pi-hole) and [Unbound](https://github.com/NLnetLabs/unbound)
- Apps in this project are deployed in [docker](https://github.com/docker) containers and manager via [Portainer](https://github.com/portainer/portainer).
- Built on a repurposed laptop acting as a home server.
- The server is being managed and administered with a mini pc via SSH.

## 📌 Project Overview
Instead of relying on a my ISPs DNS Servers or public resolvers like Cloudfare and Google DNS to resolve domain names, which means every sites visited is being visible to a third party and no protecting against Ads and trackers on a network level.

This project aims to tackle that problem with a fully self-hosted DNS stack
- `Pi-hole`: Intercepts queries from every device on the network configured with its DNS and blocks ads/trackers/suspecious sites before they load
- `Unbound`: Acts as Pi-hole's upstream resolver, instead of forwarding to a 3rd party DNS provider. It resolves queries from the root DNS servers.
- `Portainer`: An app that show the web UI of the dokcer app that helps to manage and view the status of the apps in the docker containers.

## 🛠️ Hardware Used
Server: An old laptop repurposed as a home server running debian and docker.  
(Did some config changes on to stay awake even when the lid was closed)
```
sudo nano /etc/systemd/logind.conf
HandleLidSwitch=ignore
sudo systemctl restart systemd-logind.service
```

Admin client: A mini PC used exclusively to SSH into the server for deployment and maintenance 

## ⚙️ How It Works
1. Pi-Hole - The Gateway
Every device on the network is configured (via router DHCP settings or manually) to use the Pi-hole's IP as its DNS server.
Pi-hole checks each query against its blocklists
The blocked lists I used on my pi-hole are:

`https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts`

`https://v.firebog.net/hosts/Easyprivacy.txt`

`https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Alternate%20versions%20Anti-Malware%20List/AntiMalwareHosts.txt`

Key Config choices
- `network_mode: host` — Pi-hole needs to take over port 53 in the server host to server DNS to the whole LAN.
- `FTLCONF_dns_upstreams=127.0.0.1#5335` — instead of pointing at Cloudflare/Google, Pi-hole's only upstream is the local Unbound instance.
- `FTLCONF_dns_listeningMode=all` — allows Pi-hole to accept queries from any interface, not just localhost, since other devices on the LAN need to reach it.
> [!WARNING]
> Make sure your router is under a firewall since you are permitting DNS queries from all origins, its better to double check.

- click [__here__](config/docker-compose.yml) for the full docker config file







