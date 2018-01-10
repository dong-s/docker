FROM alpine

MAINTAINER from dong-s.com by dong

ARG TZ='Asia/Shanghai'

ENV TZ $TZ
ENV SERVER_ADDR 0.0.0.0
ENV SERVER_PORT 8888
ENV PASSWORD    password
ENV METHOD      aes-256-cfb


RUN apk --update --no-cache upgrade && \
    apk --update --no-cache add python curl && \
    curl -Lk https://bootstrap.pypa.io/get-pip.py | python && \
    pip install shadowsocks

CMD ssserver -s $SERVER_ADDR -p  $SERVER_PORT -k $PASSWORD -m $METHOD

