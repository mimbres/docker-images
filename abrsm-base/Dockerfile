# Start from the official PyTorch image with CUDA 12.1 for NVIDIA GPUs
FROM pytorch/pytorch:2.3.0-cuda12.1-cudnn8-devel

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    git \
    nano \
    htop \
    ffmpeg \
    sox \
    openssh-client \
    lftp \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Use pip to install conda and other packages without using cache
RUN pip install \
    --no-cache-dir \
    conda \
    vllm \
    numpy==1.26 \
    awscli \
    "flash-attn==2.5.8" \
    --no-build-isolation

# Set the PATH to include the default location for pip-installed binaries
ENV PATH /root/.local/bin:$PATH

# Initialize conda
RUN conda init bash

# Set the working directory
WORKDIR /workspace

# Start a login shell to ensure conda is activated
CMD ["/bin/bash", "-l"]
