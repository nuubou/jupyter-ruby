FROM ubuntu:16.04

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential libbz2-dev libdb-dev \
        libreadline-dev libffi-dev libgdbm-dev liblzma-dev \
        libncursesw5-dev libreadline-dev libsqlite3-dev libssl-dev \
        zlib1g-dev uuid-dev tk-dev \
        libtool libffi-dev ruby ruby-dev make \
        libzmq-dev autoconf pkg-config \
        wget git automake && \
    apt-get clean all

WORKDIR /root
RUN wget --no-check-certificate https://www.python.org/ftp/python/3.6.7/Python-3.6.7.tgz && \
    tar xzf Python-3.6.7.tgz && \
    cd Python-3.6.7 && \
    ./configure --enable-shared --enable-optimizations && \
    make altinstall && \
    ldconfig /usr/local/lib/

RUN git clone https://github.com/zeromq/czmq  && \
    cd czmq && \
    ./autogen.sh && ./configure && make && make install
RUN gem install cztop iruby && \
    iruby register --force

RUN python3.6 -m pip install jupyter
RUN mkdir .jupyter
ADD jupyter .jupyter

EXPOSE 8888
CMD ["jupyter", "notebook"]
