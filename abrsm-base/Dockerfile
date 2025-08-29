# Start from the official PyTorch image with CUDA 12.1 for NVIDIA GPUs
FROM pytorch/pytorch:2.3.0-cuda12.1-cudnn8-devel

# Install system dependencies including nano, htop, ffmpeg, and sox
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    git \
    nano \
    htop \
    ffmpeg \
    sox \
    && rm -rf /var/lib/apt/lists/*

# === NEW METHOD START ===
# Use pip to install conda and other packages directly, avoiding shell script issues.
# This is a more robust method when base image environments are problematic.

# Step 1: Install conda and other required packages in one go.
# We also install a specific numpy version and other tools here.
RUN pip install \
    conda \
    vllm \
    numpy==1.26 \
    awscli \
    flash-attn \
    --no-build-isolation

# Step 2: Set the PATH to include the default location for pip-installed binaries.
# The user's local bin directory is typically where conda will be installed.
ENV PATH /root/.local/bin:$PATH

# Step 3: Initialize conda. This creates the necessary config files.
RUN conda init bash
# === NEW METHOD END ===


# Set the working directory inside the container
WORKDIR /workspace

# Start a bash shell when the container launches.
# The 'conda init' command modifies the .bashrc, so we start an interactive shell
# to ensure the conda environment is activated.
CMD ["/bin/bash", "-l"]
