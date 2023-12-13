FROM mcr.microsoft.com/devcontainers/miniconda:0-3

ARG DEVUSER=vscode

USER root

COPY environment_dev.yml* .devcontainer/noop.txt /tmp/conda-tmp/
RUN if [ -f "/tmp/conda-tmp/environment_dev.yml" ]; then umask 0002 \
    && /opt/conda/bin/conda env create -f /tmp/conda-tmp/environment_dev.yml; fi \
    && rm -rf /tmp/conda-tmp

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive


# Persist bash history
RUN SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/cmdhistory/.bash_history" \
    && mkdir /cmdhistory \
    && touch /cmdhistory/.bash_history \
    && chown -R ${DEVUSER} /cmdhistory \
    && echo "$SNIPPET" >> "/home/${DEVUSER}/.bashrc" \
    && echo "$SNIPPET" >> "/home/${DEVUSER}/.zshrc"

USER ${DEVUSER}

RUN echo "export PATH=/opt/conda/bin:$PATH" >> /home/${DEVUSER}/.zshrc \
    && echo "export PATH=/opt/conda/bin:$PATH" >> /home/${DEVUSER}/.bashrc

RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> /home/${DEVUSER}/.zshrc \
    && echo "conda activate base" >> /home/${DEVUSER}/.zshrc \
    && echo ". /opt/conda/etc/profile.d/conda.sh" >> /home/${DEVUSER}/.bashrc \
    && echo "conda activate base" >> /home/${DEVUSER}/.bashrc
