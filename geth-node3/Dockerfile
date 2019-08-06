FROM becram/ubuntu:base

RUN apt-get update \
     && apt-get install -y wget software-properties-common \
     && rm -rf /var/lib/apt/lists/*

WORKDIR "/root"

RUN add-apt-repository -y ppa:ethereum/ethereum

ARG binary
RUN apt-get update \
     && apt-get install -y ethereum curl
RUN curl -LSs https://raw.githubusercontent.com/gochain-io/web3/master/install.sh | sh


ARG password3
ARG privatekey3
RUN echo $password3 > ~/.accountpassword3
RUN echo $privatekey3 > ~/.privatekey3
ADD ./genesis.json ./genesis.json
RUN geth --nousb init genesis.json
RUN geth  --nousb account import --password ~/.accountpassword3  ~/.privatekey3
# RUN geth account import --password ~/.accountpassword2  ~/.privatekey2
# RUN geth --unlock 6EA0f36b4E72C8a3466C43Fd887da9Bd2D950bE3 --password ~/.accountpassword1
# RUN geth --unlock BC32587EA152Cae813e60f1797A8179FD1bfe3Ac --password ~/.accountpassword2

CMD exec geth --nousb --bootnodes "enode://$bootnodeId@$bootnodeIp:30301" \
    --networkid "15" --verbosity=4 --syncmode full --mine \
     --gasprice "0" --etherbase $address3  --unlock $address3 --password ~/.accountpassword3

EXPOSE 30303
#CMD ["/usr/bin/bash"]
