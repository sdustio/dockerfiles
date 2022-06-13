FROM ros:foxy-ros-base

# setup keys
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys D2486D2DD83DB69272AFE98867170598AF249743

# setup sources.list
RUN . /etc/os-release \
    && echo "deb http://packages.osrfoundation.org/gazebo/$ID-stable `lsb_release -sc` main" > /etc/apt/sources.list.d/gazebo-latest.list

# install gazebo packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    gazebo11 libgazebo11-dev ros-foxy-gazebo-ros-pkgs \
    && rm -rf /var/lib/apt/lists/*

# setup environment
EXPOSE 11345

# setup entrypoint
COPY ./entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]

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
    apt-get update; \
	apt-get install -y --no-install-recommends \
		ca-certificates \
		curl \
    ; \
	rm -rf /var/lib/apt/lists/*;

RUN set -eux; \
    curl -fSsLO ${SCRIPTLIBPREFIX}/common-debian.sh; \
    bash ./common-debian.sh "${INSTALL_ZSH}" "${USERNAME}" "${USER_UID}" "${USER_GID}" "${UPGRADE_PACKAGES}" "true" "true"; \
    rm ./common-debian.sh; \
    apt-get autoremove -y; apt-get clean -y; rm -rf /var/lib/apt/lists/*
