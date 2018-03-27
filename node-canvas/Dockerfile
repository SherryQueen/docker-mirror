FROM daocloud.io/centos:latest
LABEL author="56"

USER root
RUN \
  # node 安装
  yum install -y gcc gcc-c++ automake autoconf libtool make && \
  curl -O https://nodejs.org/dist/v8.10.0/node-v8.10.0-linux-x64.tar.xz && xz -d node-v8.10.0-linux-x64.tar.xz && tar -vxf node-v8.10.0-linux-x64.tar && mv node-v8.10.0-linux-x64 ~/node && rm node-v8.10.0-linux-x64.tar && ln -s /root/node/bin/node /usr/bin/node && ln -s /root/node/bin/npm /usr/bin/npm && \
  # node-canvas 依赖
  yum install cairo cairo-devel cairomm-devel libjpeg-turbo-devel pango pango-devel pangomm pangomm-devel giflib-devel -y

# 挂载点
VOLUME ["/app"]

# 拷贝 依赖目录
COPY package.json /data/

# 进入工作目录
WORKDIR /data
RUN \
  npm config set user 0 && \
  npm config set unsafe-perm true && \
  npm config set registry https://registry.npm.taobao.org && \
  npm install node-gyp -g && \
  npm install
ENV NODE_PATH /data/node_modules/
