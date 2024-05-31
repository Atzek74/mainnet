# docker build -t electrs .
#docker run -itd  --name electrs --restart always --network nodo -v $PWD/.electrs:/root/.electrs --ip=10.0.1.3 electrs
FROM debian
RUN apt update && apt -y upgrade
RUN apt install -y cargo 
RUN apt install -y clang 
RUN apt install -y cmake 
RUN apt install -y build-essential 
RUN apt install -y git 

WORKDIR /rust
RUN git clone --branch v"0.10.4"  https://github.com/romanz/electrs.git

WORKDIR /rust/electrs
RUN cargo build --locked --release
RUN install -m 0755 -o root -g root -t /usr/local/bin rust/electrs/target/release/electrs

WORKDIR /root/.electrs

CMD ["electrs","--conf","electrs.conf"]
