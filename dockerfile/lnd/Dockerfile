# docker build -t lnd .

FROM debian
RUN apt update && apt upgrade -y
RUN apt install wget -y

WORKDIR /tmp
RUN wget https://github.com/lightningnetwork/lnd/releases/download/v0.18.5-beta/lnd-linux-amd64-v0.18.5-beta.tar.gz
RUN tar -xvf lnd-linux-amd64-v0.18.5-beta.tar.gz
RUN install -m 0755 -o root -g root -t /usr/local/bin lnd-linux-amd64-v0.18.5-beta/*

WORKDIR /root/.lnd
CMD ["lnd"]
