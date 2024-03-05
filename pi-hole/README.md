Resources:

* basics: https://github.com/pi-hole/docker-pi-hole
* https://docs.pi-hole.net/docker/dhcp/
  --> Docker Pi-hole with a Macvlan network



### DHCP DNS Server

Was not available in the router's interface.

Hacky solution:  
Injecting custom JS into the interface to see hidden settings. See *drei-router-dns-settings.js*.  
Source: https://community.magenta.at/topic/7342-zte-mc801-dns-server-%C3%A4ndern/#comment-48656

➡️ did not work realiably, using pi-hole as dns now