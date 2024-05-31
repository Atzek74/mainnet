install docker:

    su -

    apt install curl -y
 
    curl -ssl https://get.docker.com | bash

add user to docker group:

    usermod -aG docker <user>

loguot

login

if use a exeternal ssd:

    parted

    select /dev/sdx

    mklabel gpt

    unit %

    mkpart primary ext4 0 100

    mkfs.ext4 /dev/sdxy


create a data dir:

    mkdir /data

edit fstab:

    blkid

    nano /etc/fstb

creates link:

    ln -s /data/dir /home/bitcoin/.dir

inizialize swarm manager:

    docker swarm init

inizialize worker node(s) if present(s):

    docker swarm join-token worker
    docker join...

create overlay nodo network:

    docker network create --driver=overlay --subnet=10.0.1.0/24 --gateway=10.0.1.254 --attachable nodo

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




copio eventuali dati

rsync -a (--remove-source-files) --progress ...
avvio container
