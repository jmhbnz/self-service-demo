FROM docker.io/ubuntu:22.04

COPY . /app

WORKDIR /app

USER root

RUN apt update && apt install --yes wget curl \
    && wget -O boost_1_79_0.tar.gz https://sourceforge.net/projects/boost/files/boost/1.79.0/boost_1_79_0.tar.gz/download \
    && tar xzvf boost_1_79_0.tar.gz 

RUN apt-get update && apt-get install --yes build-essential g++ autotools-dev libicu-dev libbz2-dev libboost-all-dev

RUN cd boost_1_79_0 &&  ./bootstrap.sh --prefix=/usr/ \
    && ./b2 \
    && ./b2 install

RUN g++ -pthread hwapp.cpp -o hwapp

CMD ["./hwapp 0.0.0.0 80"]
