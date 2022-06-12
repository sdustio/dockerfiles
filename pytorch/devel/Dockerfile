ARG CUDA=11.3.1-runtime-ubuntu20.04

FROM nvidia/cuda:${CUDA}

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


# Setup default python tools in a venv via pipx to avoid conflicts
ARG PYTHON_VERSION="3.8"
ENV PY_HOME=/usr/local/python \
    PY_BIN_DIR=/usr/local/python/bin
ENV PIPX_HOME=/usr/local/py-utils \
    PIPX_BIN_DIR=/usr/local/py-utils/bin
ENV PATH=${PATH}:${PY_BIN_DIR}:${PIPX_BIN_DIR}

RUN set -eux; \
    curl -fSsLO ${SCRIPTLIBPREFIX}/python-debian.sh; \
    bash ./python-debian.sh "${PYTHON_VERSION}" "${PY_HOME}" "${PIPX_HOME}" "${USERNAME}"; \
    rm ./python-debian.sh; \
    apt-get clean -y; rm -rf /var/lib/apt/lists/*


# [Choice] Node.js version: none, lts/*, 16, 14, 12, 10
ARG NODE_VERSION="none"
ENV NVM_DIR=/usr/local/share/nvm
ENV NVM_SYMLINK_CURRENT=true \
    PATH=${NVM_DIR}/current/bin:${PATH}

RUN set -eux; \
    curl -fSsLO ${SCRIPTLIBPREFIX}/node-debian.sh; \
    bash ./node-debian.sh "${NVM_DIR}" "${NODE_VERSION}" "${USERNAME}"; \
    rm ./node-debian.sh; \
    apt-get clean -y; rm -rf /var/lib/apt/lists/*

RUN pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu113

# [Optional] If your pip requirements rarely change, uncomment this section to add them to the image.
# COPY requirements.txt /tmp/pip-tmp/
# RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
#    && rm -rf /tmp/pip-tmp

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1
