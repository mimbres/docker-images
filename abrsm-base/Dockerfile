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

# === MODIFIED SECTION START ===
# Install Miniforge instead of Miniconda for better stability and compatibility
RUN wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh -O ~/miniforge.sh && \
    /bin/bash ~/miniforge.sh -b -p /opt/conda && \
    rm ~/miniforge.sh
# === MODIFIED SECTION END ===

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
