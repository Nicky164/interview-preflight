# Interview environment, built once by .github/workflows/image.yml and published to
# ghcr.io/nicky164/interview-env. Codespaces pull it instead of building on the spot.
FROM mcr.microsoft.com/devcontainers/python:1-3.13-bookworm

# The base image ships a Yarn apt source whose signing key has expired, which makes
# every apt-get update fail. Drop it.
RUN grep -rl yarnpkg /etc/apt/sources.list.d/ | xargs -r rm -f \
    && apt-get update \
    && rm -rf /var/lib/apt/lists/*

RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash - \
    && apt-get install -y --no-install-recommends nodejs \
    && rm -rf /var/lib/apt/lists/*

# As root, so they're on PATH for every shell (including non-interactive ssh).
RUN pip install --no-cache-dir uv \
    && npm install -g @anthropic-ai/claude-code @openai/codex \
    && npm cache clean --force

# Codespaces' workspace is on a different filesystem from uv's cache.
ENV UV_LINK_MODE=copy

COPY interview-env interview-key /usr/local/bin/
RUN chmod +x /usr/local/bin/interview-env /usr/local/bin/interview-key
