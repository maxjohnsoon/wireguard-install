### Max Johnson
# Digital Ocean
On Digital Ocean I created a new free account. On Digital Ocean I created a new droplet with Ubunut, the basic plan, and the cheapest regular Intel CPU. I also created a password for the droplet and choice a random data center.

# Docker Install
To install docker on the droplet, I used Digital Oceans console button in order to run code and followed what I had previously done to install docker on my own computer.
```
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker maxjohnson
```
# WireFuard Install
To Install Wireguard I inputted these comands on the console
```
mkdir -p ~/wireguard/
mkdir -p ~/wireguard/config/
nano ~/wireguard/docker-compose.yml
```
I then pasted in this into the docker-compose.yml file. Note that the SERVERURL variable is the public URL from Digital Ocean
```
version: "3.3"
services:
  wireguard:
    image: lscr.io/linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Chicago
      - SERVERURL=143.110.226.224 #optional
      - SERVERPORT=51820 #optional
      - PEERS= pc1,pc2,phone1 #optional
      - PEERDNS=auto #optional
      - INTERNAL_SUBNET=10.13.13.0 #optional
      - ALLOWEDIPS=0.0.0.0/0 #optional
    volumes:
      - type: bind
        source: ./config/
        target: /config/
      - type: bind
        source: /lib/modules
        target: /lib/modules
    ports:
      - 51820:51820/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    restart: unless-stopped
```
I then start WireGuard by running these lines which gave me a QR code which I was able to scan with the WireGuard IOS app
```
docker-compose up -d
docker-compose logs -f wireguard
```
I then downloaded WireGuard on my Mac and created an empty tunnel where I pasted in the text below
```
[Interface]
Address = 10.13.13.2
PrivateKey = CGwrMpzOQnCz+oJW4SR2NtEJ2IOaId6SsmESEv/hHHU=
ListenPort = 51820
DNS = 10.13.13.1

[Peer]
PublicKey = jkMjFipRZ1xHK1voWFVVz6alnZrHBTCo42nPj9NKjQ4=
Endpoint = 143.110.226.224:51820
AllowedIPs = 0.0.0.0/0
```
I found this by running the command below found in the config files
```
cat ~/wireguard/config/peer_pc1/peer_pc1.conf
```
This is what my IP address looked like with no VPN (left) and with the VPN on (right).
<img width="1680" alt="Screen Shot 2021-12-02 at 9 26 45 PM" src="https://user-images.githubusercontent.com/42543469/144540555-e3784ae3-79be-4ecc-bd7b-64766e1aa030.png">


