ARG OPENMS_TAG=latest

FROM tillenglert/oopenms_base:${OPENMS_TAG}

WORKDIR /OpenMS
RUN mkdir /thirdparty && \
    git submodule update --init THIRDPARTY && \
    cp -r THIRDPARTY/All/* /thirdparty && \
    cp -r THIRDPARTY/Linux/64bit/* /thirdparty && \
    # install msfragger
    mv /thirdparty/MSFragger/License.txt /thirdparty/License.txt && \
    mv /thirdparty/MSFragger/README.MD /thirdparty/README.MD && \
    git clone REPOSITORY/FOR/MSFRAGGER_3.2 /thirdparty/MSFragger && \  # This needs to be edited
    rm -rf /thirdparty/MSFragger/.git && \
    mv /thirdparty/License.txt /thirdparty/MSFragger/License.txt && \
    mv /thirdparty/README.MD /thirdparty/MSFragger/README.MD && \
    # install java libraries
    apt-get install wget && \
    apt-get -y update && \
    apt-get install -y openjdk-8-jdk

ENV PATH="/thirdparty/LuciPHOr2:/thirdparty/MSGFPlus:/thirdparty/Sirius:/thirdparty/ThermoRawFileParser:/thirdparty/Comet:/thirdparty/Fido:/thirdparty/MaRaCluster:/thirdparty/MyriMatch:/thirdparty/OMSSA:/thirdparty/Percolator:/thirdparty/SpectraST:/thirdparty/XTandem:/thirdparty/crux:${PATH}"
ENV MSFRAGGER_PATH="/thirdparty/MSFragger/MSFragger-3.2.jar"

WORKDIR /openms-build
RUN make TOPP && make UTILS && rm -rf src doc CMakeFiles

WORKDIR /
ENV PATH="/openms-build/bin/:${PATH}"