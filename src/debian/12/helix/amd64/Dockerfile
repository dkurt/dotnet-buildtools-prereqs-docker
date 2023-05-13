FROM mcr.microsoft.com/dotnet/runtime-deps:8.0-preview-bookworm-slim

# Install Helix Dependencies

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    python3 \
    python3-venv \
    python3-dev \
    gcc \
    && rm -rf /var/lib/apt/lists/*

# create helixbot user and give rights to sudo without password
RUN useradd --uid 1000 --shell /bin/bash --create-home --gid adm helixbot && \
    chmod 755 /root && \
    echo "helixbot ALL=(ALL)       NOPASSWD: ALL" > /etc/sudoers

ENV LANG=en-US.UTF-8

USER helixbot

ARG python3=/home/helixbot/env/bin/python3

RUN cd \
    && python3 -m venv env \
    && $python3 -m pip download --no-deps helix-scripts --index-url https://dnceng.pkgs.visualstudio.com/public/_packaging/helix-client-prod/pypi/simple \
    && $python3 -m pip install ./helix_scripts-*-py3-none-any.whl
