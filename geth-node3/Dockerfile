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

ARG password1
ARG password3
ARG privatekey1
ARG privatekey3
RUN echo $password1 > ~/.accountpassword1
RUN echo $password3 > ~/.accountpassword3
RUN echo $privatekey1 > ~/.privatekey1
RUN echo $privatekey3 > ~/.privatekey3
ADD ./genesis.json ./genesis.json
RUN geth --nousb init genesis.json
RUN geth  --nousb account import --password ~/.accountpassword1  ~/.privatekey1
RUN geth  --nousb account import --password ~/.accountpassword3  ~/.privatekey3
# RUN geth account import --password ~/.accountpassword2  ~/.privatekey2
# RUN geth --unlock 6EA0f36b4E72C8a3466C43Fd887da9Bd2D950bE3 --password ~/.accountpassword1
# RUN geth --unlock BC32587EA152Cae813e60f1797A8179FD1bfe3Ac --password ~/.accountpassword2

CMD exec geth --nousb --bootnodes "enode://$bootnodeId@$bootnodeIp:30301" \
    --networkid "15" --syncmode full --mine --verbosity 5  \
    --gasprice "0" --etherbase $address1  --unlock $address1 --password ~/.accountpassword1

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

EXPOSE 30303
#CMD ["/usr/bin/bash"]
