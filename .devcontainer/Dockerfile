# syntax=docker/dockerfile:1

ARG VARIANT="18"
ARG CAPVER="latest"
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:0-${VARIANT}

# Install some generally useful tools
RUN apt-get update \
    && apt-get -y install --no-install-recommends \
    jq procps curl git entr source-highlight wget

ARG USER_HOME=/home/node

# Install SAP CAP and support packages globally
USER node
RUN npm install -g @sap/cds-dk@$CAPVER
RUN npm install -g mbt
RUN npm install -g mta
RUN npm install -g @sap/generator-fiori
RUN npm install -g @ui5/cli
RUN npm install -g node@18.20.3
RUN git config --global --add safe.directory /workspaces/cap-local-dev-issue


# vi mode everywhere and nicer prompt 
RUN cat <<EOBASHRC >> ${USER_HOME}/.bashrc
export EDITOR=vi
set -o vi
bind -x '"\C-l": clear'
EOBASHRC

RUN echo 'export PS1=${PS1/\$ /\\\\n$ }' >> /home/node/.bashrc

WORKDIR ${USER_HOME}

# allow anybody to read/write/exec at HOME
RUN chmod -R o+rwx "${USER_HOME}"
ENV HOME=${USER_HOME}
