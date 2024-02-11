FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
    autoconf \
    automake \
    wget \
    curl \
    git \
    gnupg2 \
    subversion \
    build-essential \
    libxml2-dev \
    libncurses5-dev \
    libnewt-dev \
    uuid-dev \
    sqlite3 \
    libsqlite3-dev \
    pkg-config \
    libjansson-dev \
    libssl-dev \
    libsrtp2-dev \
    libreadline-dev \
    libopus-dev \
    libogg-dev \
    libvorbis-dev \
    libcurl4-openssl-dev \
    libedit-dev \
    liblua5.3-dev \
    libedit-dev \
    libtool \
    vim && rm -rf /var/lib/apt/lists/*

RUN wget https://downloads.asterisk.org/pub/telephony/asterisk/asterisk-20-current.tar.gz && \
    tar -zxvf asterisk-20-current.tar.gz && \
    rm -f asterisk-20-current.tar.gz && \
    mv asterisk-* /usr/src/asterisk

WORKDIR /usr/src/asterisk
# TODO: replace default configs
RUN ./configure --with-jansson-bundled --with-pjproject-bundled &&  \
    make menuselect.makeopts && \
    menuselect/menuselect --enable res_ari --enable core-sounds-en-wav --enable moh-opsound-wav menuselect.makeopts \
    make &&  \
    make install &&  \
    make samples

EXPOSE 5060/udp
EXPOSE 10000-20000/udp

CMD ["asterisk", "-f"]
