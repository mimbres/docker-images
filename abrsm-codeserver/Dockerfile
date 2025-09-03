# Base image from Kubeflow with Jupyter, PyTorch, and CUDA support.
FROM ghcr.io/kubeflow/kubeflow/notebook-servers/jupyter-pytorch-cuda-full:v1.10.0

# Define code-server version and architecture as build arguments for flexibility.
# The build environment (e.g., docker buildx) will provide TARGETARCH automatically.
ARG TARGETARCH
ARG CODESERVER_VERSION=4.96.4

# Switch to root user to install system packages.
USER root

# Set timezone and debian frontend to noninteractive.
ENV TZ=Europe/London
ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies.
RUN apt-get update && apt-get install -y --no-install-recommends \
    tzdata \
    s3fs \
    s3cmd \
    ffmpeg \
    sox \
    openssh-client \
    lftp \
    wget \
    curl \
    git \
    nano \
    tmux \
    nmon \
    p7zip-full \
    rename \
    htop \
    # Clean up apt cache
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install code-server using the provided arguments.
RUN curl -fsSL "https://github.com/coder/code-server/releases/download/v${CODESERVER_VERSION}/code-server_${CODESERVER_VERSION}_${TARGETARCH}.deb" -o /tmp/code-server.deb \
    && dpkg -i /tmp/code-server.deb \
    && rm -f /tmp/code-server.deb

# Install additional Python packages.
RUN pip install \
    --no-cache-dir \
    conda \
    numpy==1.26 \
    awscli \
    fsspec \
    aiobotocore \
    s3fs \
    boto3

# Configure PATH for packages installed by the user.
ENV PATH /home/${NB_USER}/.local/bin:$PATH

# Expose Jupyter's default port (from base image) and code-server's default port.
EXPOSE 8888 8080

# Switch back to the default non-root user.
# The NB_USER variable is defined in the base image (e.g., 'jovyan').
USER ${NB_USER}

# Set the working directory to the user's home.
WORKDIR /home/${NB_USER}

# The entrypoint from the base image will start Jupyter by default.
# To start code-server, you'll need to run it from a terminal inside the container.
