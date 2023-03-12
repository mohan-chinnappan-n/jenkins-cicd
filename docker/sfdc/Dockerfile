FROM jenkins/agent:alpine-jdk11
# author: mchinnappan

USER root
# install python3
RUN apk add python3
RUN apk add py3-pip

# install vim
RUN apk add  vim




# install nodejs and sfdx cli
RUN apk add nodejs 
RUN apk add npm 
RUN apk add yarn 



ARG SALESFORCE_CLI_VERSION=latest
RUN npm install --global sfdx-cli@${SALESFORCE_CLI_VERSION}


RUN apk add jq 

USER jenkins

# install required plugins
RUN  echo 'y' |  sfdx plugins:install sfdx-mohanc-plugins
RUN  echo 'y' |  sfdx plugins:install sfdx-git-delta



