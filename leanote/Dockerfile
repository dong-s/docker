FROM mongo:3.2

WORKDIR /home

RUN set -x && \
	rm /etc/localtime && \
    ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone && \
    apt-get update && \
    apt-get install -qq --no-install-recommends -y wget && \
    apt-get clean -qq && \
    wget http://file.dong-s.com/2019/07/leanote-linux-amd64-v2.6.1.bin.tar.gz && \
	tar -xzf leanote-linux-amd64-v2.6.1.bin.tar.gz && \
	rm -rf leanote-linux-amd64-v2.6.1.bin.tar.gz && \
    sed -i '/#!\/bin\/sh/amongod &\nif [ ! -f "\/home\/leanote\/is_init_completed" ]; then \
        mongorestore -h localhost -d leanote --dir \/home\/leanote\/mongodb_backup\/leanote_install_data\/ \
        touch \/home\/leanote\/is_init_completed\nfi\n' /home/leanote/bin/run.sh

EXPOSE 9000

CMD ["/bin/bash", "leanote/bin/run.sh"]