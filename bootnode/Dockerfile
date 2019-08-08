FROM becram/ubuntu:base

RUN apt-get update \
     && apt-get install -y wget software-properties-common \
     && rm -rf /var/lib/apt/lists/*

WORKDIR "/root"

RUN add-apt-repository -y ppa:ethereum/ethereum

ARG binary
RUN apt-get update \
     && apt-get install -y ethereum

ENV nodekeyhex=""
RUN bootnode --genkey=boot.key


# COPY ./boot.key .
#CMD exec bootnode -nodekeyhex $nodekeyhex
CMD exec bootnode --nodekey=boot.key 
#CMD exec bootnode -nodekeyhex $nodekeyhex
#CMD exec bootnode -nodekeyhex $nodekeyhex 
#CMD ["/usr/bin/bash"]

EXPOSE 30301/udp
EXPOSE 30303/udp
