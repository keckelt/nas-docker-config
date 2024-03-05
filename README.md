# NAS Services

## Local Network
Network my devices are using at home:

* Router: 192.168.0.1
* Subnet Mask: 255.255.255.0
* IP Range: 192.168.0.1 - 192.168.0.254
* DHCP Range: 192.168.0.101 - 192.168.0.199
* Devices with static IPs: 192.168.0.1 - 192.168.0.100
* DNS: 192.168.0.220 (Pi-Hole)  
  Upstream DNS:
    * OpenDNS: 208.67.222.222
    * Cloudflare: 1.1.1.1

### Docker Sub-Network
To give docker services their own IP in the network, instead of using the host IP (192.168.0.10), a macvlan network is used.
The network is created using the command below, instead of a compose file.
This way, it is independent of a particualr service and can be reused for multiple services.

* Network adress: 192.168.0.208/28  
  like 192.168.0.0 but the smaller net starts at 208, see https://jodies.de/ipcalc?host=192.168.0.208&mask1=28&mask2=
* IP Range: 192.168.0.209 - 192.168.0.222  
  i.e., unused IP range in the above network
* Broadcast (last IP in range): 192.168.0.223  
  like 192.168.0.255 but for the smaller net
* Subnet Mask: 255.255.255.240

Create the network with:
```bash
docker network create
    -d macvlan
    --gateway=192.168.0.1 # router ip
    --subnet=192.168.0.1/24  # real subnet currently in use (i.e. 192.168.0.1 - 192.168.0.255)
    --ip-range=192.168.0.219/28 # new subnet for docker services, see 
    # --aux-address="mypyhole=192.168.0.220" \ # adress specified manually as not available --> cant be used by the docker container either! Not using this here.
    -o parent=eth0 # network interface
    macvlan0
```


