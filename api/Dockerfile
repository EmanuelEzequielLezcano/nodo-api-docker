FROM ubuntu:latest

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y software-properties-common cron wget curl locales npm git zip unzip

RUN locale-gen es_AR.UTF-8
RUN export LANG=es_AR.UTF-8

RUN git clone https://gitlab.bfa.ar/blockchain/tsa2.git

RUN cd tsa2/api && npm install -g truffle && npm install

RUN cd tsa2/api && npm run build

RUN sed -i "s/chainId: '99118822',/ /g" /tsa2/api/dist/StamperWrapper.js && sed -i 's/txPromise = await this.web3.eth.sendSignedTransaction/txPromise = this.web3.eth.sendSignedTransaction/g' /tsa2/api/dist/StamperWrapper.js

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 3000

ENV GETH_ACCOUNT_JSON="/nodo_data/account.json"
ENV GETH_ACCOUNT_PASSWORD=""
ENV GETH_HOST=http://nodobfa:8545
ENV CONTRACT_ABI_PATH="tsa2/api/abi.json"
ENV CONTRACT_ADDRESS=0x7e56220069CAaF8367EA42817EA9210296AeC7c6

CMD [ "node", "tsa2/api/dist/index.js" ]
