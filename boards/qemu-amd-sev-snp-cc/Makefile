# Setup QEMU with AMD SEV SNP to run Confidential VM, and RDMA.


# vm1 starts a QEMU instance with AMD-SEV-SNP support.
#
#
# Guide: https://ubuntu.com/server/docs/how-to/virtualisation/sev-snp/
vm1: host-sev
	@echo "Hello~"
	qemu-system-x86_64 \
	  -enable-kvm \
	  -nographic \
	  -machine q35 -smp 6 -m 6G \
	  -drive "if=virtio,format=qcow2,file=images/ubuntu-24.04-server-cloudimg-amd64.img" \
	  -net nic,model=e1000 -net user,hostfwd=tcp::2222-:22 \
	  -cpu EPYC-v4 \
	  -machine memory-encryption=sev0,vmport=off \
	  -object memory-backend-memfd,id=ram1,size=6G,share=true,prealloc=false \
	  -machine memory-backend=ram1 \
	  -object sev-snp-guest,id=sev0,cbitpos=47,reduced-phys-bits=1,kernel-hashes=on,policy=0x30000 \
	  -kernel ./vmlinuz \
	  -append "root=/dev/vda1 console=ttyS0" \
	  -bios /usr/share/ovmf/OVMF.amdsev.fd

host-sev:
	@echo "Host AMD CPU need enable SEV-SNP"
	#
	# $ cat /sys/module/kvm_amd/parameters/sev
	# Y
	# $ cpuid -1 -l 0x8000001f
	# CPU:
	#    AMD Secure Encryption (0x8000001f):
	#       SME: secure memory encryption support    = true
	#       SEV: secure encrypted virtualize support = true
	#       VM page flush MSR support                = false
	#       SEV-ES: SEV encrypted state support      = true
	#       SEV-SNP: SEV secure nested paging        = true

deps:
	# https://github.com/AMDESE/AMDSEV?tab=readme-ov-file#ubuntu-1804
	#
	# Guest requires a specific version of UEFI Fiwmare
	# to enable persistant NVRAM storage, VARS.fd 
	#
	# QEMU consumes UEFI firmware in form of ovmf format, VM UEFI FW.
	
	
omvf:
	# Containerized build, depend on host with Docker.

getedk2:
	git clone --recursive https://github.com/tianocore/edk2.git; cd edk2; git submodule update --init	
