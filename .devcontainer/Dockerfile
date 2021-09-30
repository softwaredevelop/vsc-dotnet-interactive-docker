ARG REPO=mcr.microsoft.com/dotnet/sdk
FROM $REPO:latest

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID --shell /bin/bash --create-home $USERNAME

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    bash-completion
