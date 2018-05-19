FROM ubuntu:16.04

WORKDIR /root

RUN apt-get update && \
    apt-get install -y \
    wget unzip curl nano\
    build-essential pkg-config libc6-dev m4 g++-multilib \
    autoconf libtool ncurses-dev unzip git python python-zmq \
    zlib1g-dev wget curl bsdmainutils automake

RUN git clone https://github.com/zcash/zcash.git \
  && cd zcash \
  && git submodule update --init --recursive \
  && ./zcutil/fetch-params.sh \
  && ./zcutil/build.sh -j$(nproc)
  
RUN mkdir -p ~/.zcash \
    && echo "addnode=mainnet.z.cash" >~/.zcash/zcash.conf   

ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/local/lib
