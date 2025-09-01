FROM ghcr.io/kubeflow/kubeflow/notebook-servers/jupyter-pytorch-cuda-full:v1.10.0

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
    p7zip \
    htop \
    # Clean up apt cache
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

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

# Switch back to the default non-root user.
# The NB_USER variable is defined in the base image (e.g., 'jovyan').
USER ${NB_USER}

# Set the working directory to the user's home.
WORKDIR /home/${NB_USER}
