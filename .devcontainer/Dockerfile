FROM mcr.microsoft.com/devcontainers/python:1-3.13-bookworm

# The base image ships a Yarn apt source whose signing key has expired, which makes
# every apt-get update fail (and with it the devcontainer features below). Drop it.
RUN grep -rl yarnpkg /etc/apt/sources.list.d/ | xargs -r rm -f \
    && apt-get update \
    && rm -rf /var/lib/apt/lists/*

# Installed as root so it's on PATH for every shell, including non-interactive ssh.
RUN pip install --no-cache-dir uv
