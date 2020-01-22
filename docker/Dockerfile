FROM ubuntu:latest

RUN apt-get update -y && apt-get upgrade -y

WORKDIR /root/

RUN apt-get install wget autoconf libtool libboost-all-dev \
        libcurl4-openssl-dev libevent-dev libssl-dev unzip \
        nano build-essential make git pkg-config bsdmainutils -y
    
RUN wget http://download.oracle.com/berkeley-db/db-4.8.30.zip \
        && unzip db-4.8.30.zip

WORKDIR /root/db-4.8.30/dbinc

RUN awk 'NR==147 {$0="        __atomic_compare_exchange_db((p), (o), (n))"} { print }' atomic.h > atomic-rc.h \
    && awk 'NR==179 {$0="static inline int __atomic_compare_exchange_db("} { print }' atomic-rc.h > atomic-rc2.h \
    && rm atomic.h atomic-rc.h && mv atomic-rc2.h atomic.h

WORKDIR /root/db-4.8.30/build_unix/

RUN ../dist/configure --prefix=/usr/local --enable-cxx && make && make install

WORKDIR /root/

RUN git clone https://github.com/bitcoin/bitcoin.git && cd bitcoin \
        && git checkout v0.19.0.1 && git status && ./autogen.sh \
        && ./configure && make && make install

WORKDIR /root/

RUN apt-get autoremove && apt-get remove nano wget git -y\
        && rm -rf bitcoin && rm -rf db-4.8.30 && rm -rf db-4.8.30.zip \
        && echo 'export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/lib"' >> /root/.bashrc