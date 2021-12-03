## Digital Ocean
On Digital Ocean I created a new free account. On Digital Ocean I created a new droplet with Ubunut, the basic plan, and the cheapest regular Intel CPU. I also created a password for the droplet and choice a random data center.

## Docker Install
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
## Wireguard Install
To Install Wireguard I inputted these comands on the console
```
mkdir -p ~/wireguard/
mkdir -p ~/wireguard/config/
nano ~/wireguard/docker-compose.yml
```
