# docker build -t nginx .
# docker run -itd  --name nginx --restart always --network nodo --ip=10.0.1.4 -p 50002:50002 -p 4002:4002nginx

FROM debian
RUN apt update && apt upgrade -y
RUN apt install -y nginx 
RUN apt install -y libnginx-mod-stream
RUN apt install -y openssl

RUN openssl req -x509 -nodes -newkey rsa:4096 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt -subj "/CN=nodoBos" -days 3650

RUN mkdir /etc/nginx/streams-enabled
COPY ./nginx.conf /etc/nginx
COPY ./electrs-reverse-proxy.conf /etc/nginx/streams-enabled
#COPY ./rtl-reverse-proxy.conf /etc/nginx/streams-enabled

CMD ["nginx", "-g", "daemon off;"]
