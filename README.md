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

create volumes for data

	docker volume create <volume-name>

in docker-compose:

	volumes:
          <volume-name>:
    	    external: true



