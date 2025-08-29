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

# Install Miniconda (as previously requested)
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh

# Set the PATH environment variable for conda
ENV PATH /opt/conda/bin:$PATH

# Install specified Python packages using pip
# vllm will automatically detect the PyTorch/CUDA version and install the correct backend.
RUN pip install \
    vllm \
    numpy==1.26 \
    awscli \
    flash-attn \
    --no-build-isolation

# Set the working directory inside the container
WORKDIR /workspace

# Start a bash shell when the container launches
CMD ["/bin/bash"]
