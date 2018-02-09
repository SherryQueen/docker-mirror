FROM daocloud.io/centos:latest
LABEL author="56"

# 安装gcc 编译环境
RUN yum install -y gcc automake autoconf libtool make

# 安装Imagemagick 依赖
RUN yum install -y libjpeg libjpeg-devel libpng libpng-devel libgomp

# 安装Imagemagick
RUN curl -O https://www.imagemagick.org/download/ImageMagick.tar.gz && tar vxzf ImageMagick.tar.gz && rm ImageMagick.tar.gz && cd ImageMagick-7.0.7-22 && ./configure && make && make install
