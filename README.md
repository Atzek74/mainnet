install sudo:

    su -
    
    apt update
    
    apt install sudo

    usermod -aG sudo <user>

    exit

logout

login


install docker:

    sudo apt install curl -y
 
    curl -ssl https://get.docker.com | bash

add user to docker group:

    usermod -aG docker <user>

loguot

login


create nodo network :

    docker network create --driver=bridge --subnet=10.0.1.0/24 --gateway=10.0.1.254 nodo

create volumes:

    docker volume create bitcoin-data

    docker volume create electrs-data

    docker volume create lnd-data 

    docker volume create rtl-data

create tor image:

    cd dockerfile/tor
    modify the file torrc.sample
    docker build --build-arg pass=password -t tor .

test tor:

    docker compose up tor 

when tor is syncronize 100% ctrl+c

create bitcoin image:

    cd dockerfile/bitcoin
    docker build -t bitcoind .

create electrs image(require a lot of CPU):

    cd dockerfile/electrs
    docker build -t electrs .

create node image

    cd dockerfile/node
    docker build -t node .

from inside rtl-data volume

    git clone https://github.com/Ride-The-Lightning/RTL.git
    cd RTL
    git checkout v0.15.4
    
    cp Sample-RTL-Config.json ./RTL-Config.json
    nano RTL-Config.json
    
exit

    docker run --rm -it --volume --name node rtl-data:/root/.rtl node bash

    npm install --omit=dev --legacy-peer-deps

    ctrl P + Q
 
     docker stop node



#############
to complete
#############


create nginx image:

    cd dockerfile/nginx
    modify the file if needed
    docker build -t nginx .





create bitcoin.conf

    cd .bitcoin
    cp bitcoin.sample bitcoin.conf
    docker pull python
    docker run -it --rm python bash
    wget https://raw.githubusercontent.com/bitcoin/bitcoin/master/share/rpcauth/rpcauth.py
    python3 rpcauth.py admin password
    exit

    modify bitcoin.conf
    (with root user) 	cd ..
			cat .tor/bitcoin_hidden_service/hostname 
    cd .bitcoin
    modify bitcoin.conf

to copy data:

rsync -a (--remove-source-files) --progress ...




from rtl-vololume:

clone repository

git checkout

cp Sample-RTL-Config.json ./RTL-Config.json

nano RTL-Config.json

docker run --rm -it --volume rtl-data:/root/.rtl node bash

npm install --omit=dev --legacy-peer-deps

ctrl P + Q


