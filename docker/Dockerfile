FROM maven:3-openjdk-8

ARG MBT_VERSION=1.0.15

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y npm make

RUN wget https://github.com/SAP/cloud-mta-build-tool/releases/download/v${MBT_VERSION}/cloud-mta-build-tool_${MBT_VERSION}_Linux_amd64.tar.gz -O - | tar xzf - mbt && mv mbt /usr/local/bin/
RUN npm config set strict-ssl false &&\
    npm config set @sap:registry https://npm.sap.com &&\
    npm install --global @ui5/cli

ADD xs /usr/local/xs
RUN chmod +x /usr/local/xs/bin/xs &&\
    chmod +x /usr/local/xs/sapjvm_8_jre/bin/java

ENV PATH="/usr/local/xs/bin/:${PATH}"

CMD echo 52.137.35.248 hxehost >> /etc/hosts; supervisord -n;