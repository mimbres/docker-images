# Start from the official PyTorch image with CUDA 12.6 for NVIDIA GPUs w/o flash-attn
FROM pytorch/pytorch:2.6.0-cuda12.6-cudnn9-devel

# Set the timezone to Europe/London to avoid interactive prompts during package installation
ENV TZ=Europe/London
# Set debian frontend to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    # Install tzdata first to configure timezone
    tzdata \
    # File IO dependencies
    s3fs \
    s3cmd \
    # Media Codec
    ffmpeg \
    sox \
    # Network
    openssh-client \
    lftp \
    # Others
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

# Use pip to install conda and other packages without using cache
RUN pip install \
    --no-cache-dir \
    conda \
    numpy==1.26 \
    awscli \
    fsspec \
    aiobotocore \
    s3fs \
    boto3 \
    --no-build-isolation

# Set the PATH to include the default location for pip-installed binaries
ENV PATH /root/.local/bin:$PATH

# Initialize conda
RUN conda init bash

# Set the working directory
WORKDIR /workspace

# Start a login shell to ensure conda is activated
CMD ["/bin/bash", "-l"]
