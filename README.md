# wireguard
1) Sign up for a new account on Digital Ocean and get your $200 free credit
2) Create a basic Ubuntu 20.04 regular intel CPU droplet
3) Open the console and install necessary tools with the command sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
4) Add a docker key using "curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -"
5) Add a docker repo using "sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable""
6) Switch to correct repo using "apt-cache policy docker-ce"
7) Install docker using "sudo apt install docker-ce -y"
8) Install docker compose using "sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose"
9) Set permissions using "sudo chmod +x /usr/local/bin/docker-compose"
10) Make a wireguard directory using "mkdir -p ~/wireguard/"
11) Make a config directory using "mkdir -p ~/wireguard/"
12) Edit the docker compose file using "nano ~/wireguard/docker-compose.yml"
13) Copy this text into the file
version: '3.8'
services:
  wireguard:
    container_name: wireguard
    image: linuxserver/wireguard
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Chicago
      - SERVERURL=64.23.128.177
      - SERVERPORT=51820
      - PEERS=pc1,pc2,phone1
      - PEERDNS=auto
      - INTERNAL_SUBNET=10.0.0.0
    ports:
      - 51820:51820/udp
    volumes:
      - type: bind
        source: ./config/
        target: /config/
      - type: bind
        source: /lib/modules
        target: /lib/modules
    restart: always
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
14) Change directory into the wireguard directory "cd ~/wireguard/"
15) Start up wireguard with "docker-compose up -d"
16) Download the wireguard app on a mobile device
17) Hit the plus then scan a QR code
18) Enter this code in the droplet console to get the QR code "docker-compose logs -f wireguard"
19) Activate the VPN and go to iplink.net to see if your IP has changed
20) Now to activate it on a laptop go to the droplet console and navigate to the config file
21) Open the file using nano and copy all the text
22) Create a config file in vscode and paste the text and save it
23) Download the Wireguard app on your laptop and choose the file that you saved from VScode
24) Click the activate button to activate the VPN and check IPleak.net to see if your IP has changed




![unnamed](https://github.com/Dawsonrep/wireguard/assets/124703437/7edf4013-2602-40f0-b7aa-911ab5918a93)

![unnamed (1)](https://github.com/Dawsonrep/wireguard/assets/124703437/cf1c2df7-e181-4755-8ae3-b7d0d6b37073)


![unnamed (2)](https://github.com/Dawsonrep/wireguard/assets/124703437/f8b0b602-679c-4b3d-b467-0155c024b0c7)

![unnamed (3)](https://github.com/Dawsonrep/wireguard/assets/124703437/7249e8d8-8f35-41ec-b74e-1b97108c91c3)




















