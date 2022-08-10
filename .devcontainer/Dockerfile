# [Choice] Debian version (use bullseye on local arm64/Apple Silicon): bullseye, buster
ARG VARIANT="bullseye"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

ARG REMOTE_USER=vscode
# ** [Optional] Uncomment this section to install additional packages. **
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
RUN mkdir -p /home/$REMOTE_USER/.vscode-server/extensions \
        /home/$REMOTE_USER/.aws /home/$REMOTE_USER/.kube \
    && chown -R $REMOTE_USER /home/$REMOTE_USER/.vscode-server \
        /home/$REMOTE_USER/.aws /home/$REMOTE_USER/.kube

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends bash-completion binutils \
    # Clean up
    && rm -rf /tmp/tmp.* \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Switch back to dialog for any ad-hoc use of apt-get
ENV DEBIAN_FRONTEND=
