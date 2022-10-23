FROM prvst/philosopher

USER root

WORKDIR /thirdparty

RUN apt-get install wget && \
    apt-get -y update && \
    apt-get install -y openjdk-8-jdk && \
    # install CrystalC
    wget https://github.com/Nesvilab/Crystal-C/releases/download/1.4.2/CrystalC-1.4.2.jar && \
    mkdir CrystalC && \
    mv CrystalC-1.4.2.jar CrystalC/CrystalC-1.4.2.jar && \
    # install PTMShepherd
    wget https://github.com/Nesvilab/PTM-Shepherd/releases/download/v1.1.1/ptmshepherd-CLI-1.1.1.jar && \
    mkdir PTMShepherd && \
    mv ptmshepherd-CLI-1.1.1.jar PTMShepherd/ptmshepherd-CLI-1.1.1.jar

ENV PATH="/thirdparty/CrystalC:/thirdparty/PTMShepherd:${PATH}"
