FROM ghcr.io/sdustio/ros2:base

# For VSCode devcontainer

# [Option] Install zsh
ARG INSTALL_ZSH="true"
# [Option] Upgrade OS packages to their latest versions
ARG UPGRADE_PACKAGES="true"
# Install needed packages and setup non-root user. Use a separate RUN statement to add your own dependencies.
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

ENV SCRIPTLIBPREFIX="https://raw.githubusercontent.com/microsoft/vscode-dev-containers/v0.238.0/script-library/"

RUN set -eux; \
    curl -fSsLO ${SCRIPTLIBPREFIX}/common-debian.sh; \
    bash ./common-debian.sh "${INSTALL_ZSH}" "${USERNAME}" "${USER_UID}" "${USER_GID}" "${UPGRADE_PACKAGES}" "true" "true"; \
    rm ./common-debian.sh; \
    apt-get autoremove -y; apt-get clean -y; rm -rf /var/lib/apt/lists/*

CMD [ "sleep", "infinity" ]
