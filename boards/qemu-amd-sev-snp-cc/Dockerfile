FROM ghcr.io/tianocore/containers/ubuntu-22-dev:latest

# Install build dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    uuid-dev \
    iasl \
    nasm \
    python3 \
    git \
    qemu-system-x86 \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y grub2-common
RUN apt-get install -y build-essential git uuid-dev iasl nasm python3 python3-distutils gcc

# Build command (example)
# RUN make -C BaseTools

# Build the AMD SEV Firmware for Qemu.
# RUN build -p OvmfPkg/AmdSev/AmdSevX64.dsc -a X64 -b RELEASE -t GCC5
# RUN md5sum Build/AmdSev/RELEASE_GCC5/FV/OVMF.fd
