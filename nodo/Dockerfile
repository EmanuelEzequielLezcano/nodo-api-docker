FROM ubuntu:latest

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y software-properties-common cron wget curl locales npm git zip unzip net-tools nano

RUN locale-gen es_AR.UTF-8
RUN export LANG=es_AR.UTF-8

RUN git clone https://gitlab.bfa.ar/blockchain/nucleo.git /bfa

RUN mkdir -p /nodo_data/

RUN /bfa/bin/installbfa.sh

RUN chown bfa:bfa -R /nodo_data/

RUN sed -i 's/--rpccorsdomain \\\*/--rpccorsdomain \\\* \\\n --rpcaddr 0.0.0.0\t\\\n --rpcport 8545/g' /home/bfa/bfa/bin/start.sh

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER bfa

RUN export BFAHOME=/home/bfa/bfa && PATH=${PATH}:/home/bfa/bfa/bin:/home/bfa/bin && admin.sh account

RUN cp /home/bfa/bfa/network/node/keystore/UTC* /nodo_data/account.json

VOLUME /nodo_data/

EXPOSE 8545 8546 30303

ENTRYPOINT ["/bin/sh", "-c" , "/home/bfa/bfa/bin/start.sh && tail -F /dev/null"]
