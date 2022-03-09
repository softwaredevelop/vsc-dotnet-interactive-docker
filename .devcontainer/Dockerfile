ARG VARIANT=6.0-bullseye-slim
FROM mcr.microsoft.com/dotnet/sdk:$VARIANT

RUN apt-get update \
    && apt-get install --no-install-recommends --assume-yes \
    sudo \
    locales \
    && apt-get clean && rm -fr /var/lib/apt/lists/*

RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --gid $USER_GID \
    --create-home $USERNAME \
    --shell /bin/bash \
    --uid $USER_UID \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

RUN mkdir /commandhistory \
    && touch /commandhistory/.bash_history \
    && chown --recursive $USERNAME /commandhistory \
    && echo "export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" >> /home/$USERNAME/.bashrc

RUN mkdir --parents /home/$USERNAME/.vscode-server/extensions \
    # /home/$USERNAME/.vscode-server-insiders/extensions \
    && chown --recursive $USERNAME \
    /home/$USERNAME/.vscode-server
# /home/$USERNAME/.vscode-server-insiders

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    bash-completion \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
