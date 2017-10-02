FROM jenkins

USER root

RUN apt-get update && \
    curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
    apt-get install -y nodejs

RUN npm install hexo-cli@1.0.3 -g

RUN mkdir /hexo && \
    chown jenkins:jenkins /hexo

USER jenkins

RUN cd /hexo && \
    hexo init . && \
    npm install hexo-generator-searchdb --save

