# ROCm Installation Tutorial

Reading Time: 15 minutes

## Introduction

### What is ROCm?

**ROCm** (Radeon Open Compute) is an open-source software platform from AMD designed for high-performance computing (HPC), machine learning, and scientific computing on AMD GPUs. ROCm is designed to enable a full-stack approach for applications using AMD GPUs, allowing developers to run code on GPUs using APIs like OpenCL, HIP (Heterogeneous Interface for Portability), and more.

**ROCm provides**:
- **GPU-Accelerated Libraries**: Libraries like **rocBLAS**, **rocFFT**, and **MIOpen** offer optimized implementations for scientific computing, machine learning, and AI tasks.
- **Support for AMD GPUs**: While OpenCL can run on AMD GPUs, ROCm provides deeper integration and performance optimizations for AMD hardware.
- **Machine Learning Support**: ROCm includes libraries like **TensorFlow** and **PyTorch** for AMD GPUs, although the ecosystem is still developing compared to CUDA.

---

## Installation Steps

Follow the steps below to install**ROCm** on your Ubuntu system.

### Update and Install Dependencies

Update your package list and install the necessary dependencies. **This is for Ubuntu 24.04 LTS**. For general, refer to the [ROCm Installation Guide](https://rocm.docs.amd.com/projects/install-on-linux/en/latest/install/quick-start.html).

```bash
sudo apt update
sudo apt install "linux-headers-$(uname -r)" "linux-modules-extra-$(uname -r)"
sudo apt install python3-setuptools python3-wheel
sudo usermod -a -G render,video $LOGNAME # Add the current user to the render and video groups
wget https://repo.radeon.com/amdgpu-install/6.3.2/ubuntu/jammy/amdgpu-install_6.3.60302-1_all.deb
sudo apt install ./amdgpu-install_6.3.60302-1_all.deb
sudo apt update
sudo apt install amdgpu-dkms rocm
```

This installation will install the necessary drivers and libraries for AMD GPUs on your system. However, large space (around 35 GB) is required for the installation.

### Verify Installation

Verify the installation by running the following command:

```bash
rocminfo
clinfo
apt list --installed | grep rocm
```

## Install PyTorch with ROCm Support

### Using a Docker Image with PyTorch Pre-Installed

This guide will walk you through using a **Docker** container with **PyTorch** pre-installed and **ROCm** support for AMD GPUs. This approach makes it easy to get started with deep learning on an AMD GPU without the need for complex installation steps.

#### Prerequisites

- A system with **Docker** installed.
- An AMD GPU compatible with **ROCm**.
- **ROCm** already set up on your system (as outlined in the previous tutorial).
- Proper driver setup for your AMD GPU.

#### Steps
1. **Pull the PyTorch Docker Image**: You can pull the **PyTorch** Docker image with **ROCm** support from the **ROCm** repository on Docker Hub. Run the following command to pull the image:

```bash
docker pull rocm/pytorch:latest
```
2. **Run the Docker Container**: Once the image is downloaded, you can run a container with the following command:

```bash
docker run -it --cap-add=SYS_PTRACE --security-opt seccomp=unconfined \
--device=/dev/kfd --device=/dev/dri --group-add video \
--ipc=host --shm-size 8G rocm/pytorch:latest

```

## Install TensorFlow with ROCm Support

(Todo)

### Using a Docker Image with TensorFlow Pre-Installed

(Todo)
