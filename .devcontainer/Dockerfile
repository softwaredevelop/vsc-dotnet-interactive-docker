ARG REPO=mcr.microsoft.com/dotnet/sdk
FROM $REPO:latest

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID --shell /bin/bash --create-home $USERNAME

RUN SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" \
    && mkdir /commandhistory \
    && touch /commandhistory/.bash_history \
    && chown --recursive $USERNAME /commandhistory \
    && echo $SNIPPET >> "/home/$USERNAME/.bashrc"

RUN mkdir --parents /home/$USERNAME/.vscode-server/extensions \
    # /home/$USERNAME/.vscode-server-insiders/extensions \
    && chown --recursive $USERNAME \
    /home/$USERNAME/.vscode-server
# /home/$USERNAME/.vscode-server-insiders

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    bash-completion
