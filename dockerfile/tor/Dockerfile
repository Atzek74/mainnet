# docker build --build-arg pass=password -t tor .
# docker run -itd  --name tor --restart always --network nodo --ip=10.0.1.1 -v $PWD/.tor:/var/lib/tor/ tor

FROM debian
RUN apt update && apt -y upgrade
RUN apt install -y wget && apt install -y gpg && apt install -y apt-transport-https
COPY tor.list /etc/apt/sources.list.d/
RUN wget -qO- https://deb.torproject.org/torproject.org/A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89.asc | gpg --dearmor | tee /usr/share/keyrings/tor-archive-keyring.gpg >/dev/null
RUN apt update && apt -y upgrade
RUN apt install -y tor deb.torproject.org-keyring

COPY torrc.sample /etc/tor/torrc

ARG pass=password
RUN sed -i s/HashedControlPassword/"HashedControlPassword "$(tor --hash-password $pass | tail -n 1)/g /etc/tor/torrc

CMD ["tor"]
