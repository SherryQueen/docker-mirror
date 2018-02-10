FROM daocloud.io/centos:latest
LABEL author="56"

# 安装gcc 编译环境
RUN yum install -y gcc automake autoconf libtool make

# 安装Imagemagick 依赖
RUN yum install -y libjpeg libjpeg-devel libpng libpng-devel libgomp

# 安装Imagemagick
RUN curl -O https://www.imagemagick.org/download/ImageMagick.tar.gz && tar vxzf ImageMagick.tar.gz && rm ImageMagick.tar.gz && cd ImageMagick-7.0.7-22 && ./configure && make && make install


# 安装node 环境
RUN curl -O https://nodejs.org/dist/v8.9.4/node-v8.9.4-linux-x64.tar.xz && xz -d node-v8.9.4-linux-x64.tar.xz && tar -vxf node-v8.9.4-linux-x64.tar && mv node-v8.9.4-linux-x64 ~/node && rm node-v8.9.4-linux-x64.tar && ln -s /root/node/bin/node /usr/bin/node && ln -s /root/node/bin/npm /usr/bin/npm

# 安装node-canvas依赖
RUN yum install -y cairo cairo-devel cairomm-devel libjpeg-turbo-devel pango pango-devel pangomm pangomm-devel giflib-devel


# 挂载点
VOLUME ["/app"]

# 进入工作目录
WORKDIR /app

# 安装依赖命令
RUN npm i

# 暴露的端口
EXPOSE 3333

# 启动命令
CMD ["npm", "run start"]