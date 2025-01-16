FROM arm64v8/ubuntu:focal

ENV DEBIAN_FRONTEND=noninteractive

## ffmpeg
RUN \
    apt update && \
    apt install -y curl wget && \
    wget https://github.com/MarcA711/Rockchip-FFmpeg-Builds/releases/download/6.1-6/ffmpeg -O /usr/bin/ffmpeg && \
    chmod +x /usr/bin/ffmpeg

## nginx-rtmp
RUN \
    apt install -y nginx libnginx-mod-rtmp && \
    cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bkp

RUN \
    mkdir -p /opt/data && \
    mkdir -p /opt/data/hls && \
    mkdir -p /www/static

COPY ${PWD}/nginx.conf /etc/nginx/nginx.conf
COPY ${PWD}/static/. /www/static
COPY ${PWD}/index.html /www/static 
COPY ${PWD}/index.html /opt/data 
COPY ${PWD}/index.html /opt/data/hls

RUN \
    chown nobody:65534 -R /opt/data && \
    chown nobody:65534 -R /www && \
    chmod 775 -R /opt/data && \
    chmod 775 -R /www

CMD nginx