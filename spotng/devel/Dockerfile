# [Choice] Debian / Ubuntu version (use Debian 11, Ubuntu 18.04/22.04 on local arm64/Apple Silicon): debian-11, debian-10, ubuntu-22.04, ubuntu-20.04, ubuntu-18.04
ARG VARIANT=ubuntu
FROM mcr.microsoft.com/vscode/devcontainers/cpp:${VARIANT}

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends ccache clang-format cppcheck valgrind \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN set -eux; \
    vcpkg install eigen3 spdlog gtest --binarysource=clear; \
    rm -rf $VCPKG_ROOT/buildtrees $VCPKG_DOWNLOADS/*
