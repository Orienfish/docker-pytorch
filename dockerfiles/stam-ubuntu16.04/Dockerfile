FROM ubuntu:16.04

# Install some basic utilities
RUN apt-get update && apt-get install -y \
    curl \
    ca-certificates \
    sudo \
    git \
    bzip2 \
    libx11-6 \
    gcc \
 && rm -rf /var/lib/apt/lists/*

# Create a working directory
RUN mkdir /app
WORKDIR /app

# Create a non-root user and switch to it
RUN adduser --disabled-password --gecos '' --shell /bin/bash user \
 && chown -R user:user /app
RUN echo "user ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/90-user
USER user

# All users can use /home/user as their home directory
ENV HOME=/home/user
RUN chmod 777 /home/user

# Install Miniconda and Python 3.6
ENV CONDA_AUTO_UPDATE_CONDA=false
ENV PATH=/home/user/miniconda/bin:$PATH
RUN curl -sLo ~/miniconda.sh https://repo.continuum.io/miniconda/Miniconda3-4.7.12.1-Linux-x86_64.sh \
 && chmod +x ~/miniconda.sh \
 && ~/miniconda.sh -b -p ~/miniconda \
 && rm ~/miniconda.sh \
 && conda install -y python==3.6.9 \
 && conda clean -ya

# No CUDA-specific steps
ENV NO_CUDA=1
RUN conda install -y -c pytorch \
    cpuonly \
    "pytorch=1.4.0=py3.6_cpu_0" \
    "torchvision=0.5.0=py36_cpu" \
 && conda clean -ya
RUN python3 -m pip install imageio==2.8.0 \
  Keras==2.3.1 \
  kmodes==0.10.2 \
  matplotlib==3.2.1 \
  networkx==2.4 \
  numpy==1.18.4 \
  opencv-python==4.2.0.32 \
  pandas==1.0.1 \
  Pillow==7.1.2 \
  progressbar33==2.4 \
  pylint==2.5.2 \
  PyYAML==5.3 \
  quadprog \
  requests==2.18.4 \
  scikit-learn==0.22.2.post1 \
  scipy==1.4.1 \
  seaborn==0.10.0 \
  tensorboard==1.14.0 \
  torch==1.4.0 \
  torchvision==0.5.0 \
  tqdm==4.43.0 \
  scikit-image \
  numba==0.50.0

# Set the default command to python3
CMD ["python3"]
