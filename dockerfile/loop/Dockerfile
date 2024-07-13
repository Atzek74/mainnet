FROM debian
RUN apt update -y && apt upgrade -y
RUN apt install -y wget
RUN wget https://github.com/lightninglabs/loop/releases/download/v0.28.5-beta/loop-linux-amd64-v0.28.5-beta.tar.gz
RUN tar -xvf loop-linux-amd64-v0.28.5-beta.tar.gz
RUN install -m 0755 -o root -g root -t usr/local/bin /loop-linux-amd64-v0.28.5-beta/*
CMD ["loopd"]
