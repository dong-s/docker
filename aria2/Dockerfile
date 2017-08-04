FROM alpine

RUN apk add --no-cache aria2

VOLUME /data
VOLUME /conf
EXPOSE 6800

RUN touch /conf/aria2.conf
RUN touch /conf/aria2.session

CMD ["aria2c", "--conf-path=/conf/aria2.conf", "--enable-rpc", "--rpc-listen-all=true", "--rpc-allow-origin-all", "input-file=/conf/aria2.session", "save-session=/conf/aria2.session"]
