# Start with the official VS Code development container
FROM mcr.microsoft.com/vscode/devcontainers/base:bullseye

# Switch to root to install dependencies
USER root

# Update system and install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \  
    curl \
    git \
    # Clean up the apt cache to reduce image size
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Bun
RUN curl -fsSL https://bun.sh/install | bash

# Add Bun to PATH
ENV PATH="/root/.bun/bin:${PATH}"

# Copy Bun to a common location accessible by any user and update PATH
RUN cp -r /root/.bun /usr/local/ && \
    echo "export PATH=/usr/local/.bun/bin:\$PATH" >> /etc/profile

# Set health check to NONE to avoid VS Code trying to run it
HEALTHCHECK NONE

# Switch back to vscode user for safety and compatibility with VS Code dev container
USER vscode