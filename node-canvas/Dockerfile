FROM daocloud.io/centos:latest
MAINTAINER 56

# 安装node 环境
RUN curl -O https://nodejs.org/dist/v8.9.4/node-v8.9.4-linux-x64.tar.xz && xz -d node-v8.9.4-linux-x64.tar.xz && tar -vxf node-v8.9.4-linux-x64.tar && mv node-v8.9.4-linux-x64 ~/node && rm node-v8.9.4-linux-x64.tar && ln -s /root/node/bin/node /usr/bin/node && ln -s /root/node/bin/npm /usr/bin/npm
