FROM node:8.11.2-alpine
LABEL author="56"

# 安装基础依赖
RUN \
  apk update && \
  apk upgrade && \
  apk add git g++ gcc libgcc libstdc++ linux-headers make python

# 安装libsass
RUN \  
  git clone https://github.com/sass/sassc && cd sassc && \
  git clone https://github.com/sass/libsass && \
  SASS_LIBSASS_PATH=/sassc/libsass make && \
  mv bin/sassc /usr/bin/sassc && \
  cd ../ && rm -rf /sassc

# 安装node-sass
ENV SASS_BINARY_PATH=/usr/lib/node_modules/node-sass/build/Release/binding.node
RUN \
  git clone --recursive https://github.com/sass/node-sass.git && \
  cd node-sass && \
  git submodule update --init --recursive && \
  npm install && \
  node scripts/build -f && \
  cd ../ && rm -rf node-sass

# 将node-sass加入.npmrc
RUN touch $HOME/.npmrc && echo "sass_binary_cache=${SASS_BINARY_PATH}" >> $HOME/.npmrc

# npm 安装时 跳过node-sass
ENV SKIP_SASS_BINARY_DOWNLOAD_FOR_CI true
ENV SKIP_NODE_SASS_TESTS true
