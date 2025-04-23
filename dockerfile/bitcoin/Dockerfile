# docker build -t bitcoind .


FROM debian
RUN apt update && apt upgrade -y
RUN apt install wget -y
RUN apt install -y python3 

WORKDIR /tmp
RUN wget https://bitcoincore.org/bin/bitcoin-core-28.1/bitcoin-28.1-x86_64-linux-gnu.tar.gz 
RUN tar -xvf bitcoin-27.0-x86_64-linux-gnu.tar.gz 
RUN install -m 0755 -o root -g root -t /usr/local/bin bitcoin-27.0/bin/*

WORKDIR /root/.bitcoin
CMD ["bitcoind"]
