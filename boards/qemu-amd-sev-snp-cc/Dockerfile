#FROM ghcr.io/tianocore/containers/ubuntu-22-dev:latest
FROM docker pull ghcr.io/tianocore/containers/ubuntu-22-dev:34f8c50

RUN apt-get update && apt-get install -y \
    grub2-common \
    build-essential \
    git \
    uuid-dev \
    iasl \
    nasm \
    python3 \
    python3-distutils \
    gcc

# Build command (example)
# RUN make -C BaseTools

# Build the AMD SEV Firmware for Qemu.
# RUN build -p OvmfPkg/AmdSev/AmdSevX64.dsc -a X64 -b RELEASE -t GCC5
# RUN md5sum Build/AmdSev/RELEASE_GCC5/FV/OVMF.fd
