# docker build -t bitcoind .
#
# cd tor-bitcoin
# 
# docker run -itd  --name bitcoind --restart always --network nodo --ip=10.0.1.2 -v $PWD/.bitcoin:/root/.bitcoin bitcoind


FROM debian
RUN apt update && apt upgrade -y
RUN apt install wget -y
RUN apt install -y python3 

WORKDIR /tmp
RUN wget https://bitcoincore.org/bin/bitcoin-core-27.0/bitcoin-27.0-x86_64-linux-gnu.tar.gz 
RUN tar -xvf bitcoin-27.0-x86_64-linux-gnu.tar.gz 
RUN install -m 0755 -o root -g root -t /usr/local/bin bitcoin-27.0/bin/*

WORKDIR /root/.bitcoin
CMD ["bitcoind"]
