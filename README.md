install docker:

    su -

    apt install curl -y
 
    curl -ssl https://get.docker.com | bash

add user to docker group:

    usermod -aG docker <user>

loguot

login



inizialize swarm in the MANAGER node !!!:

    docker swarm init

create overlay nodo network (ONLY FOR THE MANAGER NODE!!!!!):

    docker network create --driver=overlay --subnet=10.0.1.0/24 --gateway=10.0.1.254 --attachable nodo


inizialize WORKER!!! node(s) if present(s):

    run in manager node: docker swarm join-token worker
    run the output on worker node

run a busybox container in the WORKER node:

    docker run -it -d --network nodo --ip <ip address> busybo


create tor image:

    cd dockerfile/tor
    modify the file torrc.sample
    docker build --build-arg pass=password -t tor .

test tor:

from mainnet directory run:

    docker run -it --rm  --name tor --network nodo --ip=10.0.1.1 -v $PWD/.tor:/var/lib/tor/ tor 

when tor is syncronize 100% ctrl+c

create bitcoin image:

    cd dockerfile/bitcoin
    docker build -t bitcoind .

create electrs image(require a lot of CPU):

    cd dockerfile/electrs
    docker build -t electrs .

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

#############
to complete
#############

to copy data:

rsync -a (--remove-source-files) --progress ...

create volumes for data

	docker volume create <volume-name>

 	in docker-compose:
  		volumes:
  		  <volume-name>:
    		    external: true



