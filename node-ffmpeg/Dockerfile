FROM daocloud.io/centos:latest
LABEL author="56"

RUN \
  # 安装node 环境
  curl -O https://nodejs.org/dist/v8.9.4/node-v8.9.4-linux-x64.tar.xz && \
  xz -d node-v8.9.4-linux-x64.tar.xz && \
  tar -vxf node-v8.9.4-linux-x64.tar && \
  mv node-v8.9.4-linux-x64 ~/node && \
  ln -s /root/node/bin/node /usr/bin/node && \
  ln -s /root/node/bin/npm /usr/bin/npm && \
  rm node-v8.9.4-linux-x64.tar && \
  # 安装ffmpeg
  # 添加 epel源
  yum install -y epel-release && \
  # 安装nasm最新版本
  yum-config-manager --add-repo http://www.nasm.us/nasm.repo && \
  # 安装依赖
  yum install -y autoconf automake bzip2 cmake freetype-devel gcc gcc-c++ git libtool make nasm yasm mercurial pkgconfig zlib-devel && \
  mkdir ~/ffmpeg_sources && \
  # libx264
  cd ~/ffmpeg_sources && \
  git clone --depth 1 http://git.videolan.org/git/x264 && \
  cd x264 && \
  PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" --enable-static && \
  make && \
  make install && \
  make clean && \
  # libx265
  cd ~/ffmpeg_sources && \
  hg clone https://bitbucket.org/multicoreware/x265 && \
  cd ~/ffmpeg_sources/x265/build/linux && \
  cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX="$HOME/ffmpeg_build" -DENABLE_SHARED:bool=off ../../source && \
  make && \
  make install && \
  make clean && \
  # libfdk_aac
  cd ~/ffmpeg_sources && \
  git clone --depth 1 https://github.com/mstorsjo/fdk-aac && \
  cd fdk-aac && \
  autoreconf -fiv && \
  ./configure --prefix="$HOME/ffmpeg_build" --disable-shared && \
  make && \
  make install && \
  make clean && \
  # libmp3lame
  cd ~/ffmpeg_sources && \
  curl -O -L https://nchc.dl.sourceforge.net/project/lame/lame/3.100/lame-3.100.tar.gz && \
  tar xzvf lame-3.100.tar.gz && \
  cd lame-3.100 && \
  ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" --disable-shared --enable-nasm && \
  make && \
  make install && \
  make clean && \
  # libopus
  cd ~/ffmpeg_sources && \
  curl -O -L http://archive.mozilla.org/pub/opus/opus-1.2.1.tar.gz && \
  tar xzvf opus-1.2.1.tar.gz && \
  cd opus-1.2.1 && \
  ./configure --prefix="$HOME/ffmpeg_build" --disable-shared && \
  make && \
  make install && \
  make clean && \
  # libogg
  cd ~/ffmpeg_sources && \
  curl -O -L https://downloads.xiph.org/releases/ogg/libogg-1.3.3.tar.gz && \
  tar xzvf libogg-1.3.3.tar.gz && \
  cd libogg-1.3.3 && \
  ./configure --prefix="$HOME/ffmpeg_build" --disable-shared && \
  make && \
  make install && \
  make clean && \
  # libvorbis
  cd ~/ffmpeg_sources && \
  curl -O -L http://downloads.xiph.org/releases/vorbis/libvorbis-1.3.5.tar.gz && \
  tar xzvf libvorbis-1.3.5.tar.gz && \
  cd libvorbis-1.3.5 && \
  ./configure --prefix="$HOME/ffmpeg_build" --with-ogg="$HOME/ffmpeg_build" --disable-shared && \
  make && \
  make install && \
  make clean && \
  # libvpx
  cd ~/ffmpeg_sources && \
  curl -O -L http://www.loongnix.org/cgit/libvpx/snapshot/libvpx-1.7.0.tar.gz && \
  tar xzvf libvpx-1.7.0.tar.gz && \
  cd libvpx-1.7.0 && \
  ./configure --prefix="$HOME/ffmpeg_build" --disable-examples --disable-unit-tests --enable-vp9-highbitdepth --as=yasm && \
  make && \
  make install && \
  make clean && \
  # ffmpeg
  cd ~/ffmpeg_sources && \
  curl -O -L https://ffmpeg.org/releases/ffmpeg-snapshot.tar.bz2 && \
  tar xjvf ffmpeg-snapshot.tar.bz2 && \
  cd ffmpeg && \
  PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure \
  --prefix="$HOME/ffmpeg_build" \
  --pkg-config-flags="--static" \
  --extra-cflags="-I$HOME/ffmpeg_build/include" \
  --extra-ldflags="-L$HOME/ffmpeg_build/lib" \
  --extra-libs=-lpthread \
  --extra-libs=-lm \
  --bindir="$HOME/bin" \
  --enable-gpl \
  --enable-libfdk_aac \
  --enable-libfreetype \
  --enable-libmp3lame \
  --enable-libopus \
  --enable-libvorbis \
  --enable-libvpx \
  --enable-libx264 \
  --enable-libx265 \
  --enable-nonfree && \
  make && \
  make install && \
  make distclean && \
  hash -r && \
  # 清理
  yum clean all && rm -rf ~/ffmpeg_sources && \
  # 添加ffmpeg 到环境变量
  export PATH=$PATH:/root/bin
