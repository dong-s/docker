FROM alpine

RUN apk add --no-cache aria2

VOLUME /data

EXPOSE 6800

CMD ["aria2c", "--dir=/data", "--enable-rpc", "--rpc-listen-all=true", "--rpc-allow-origin-all"]
