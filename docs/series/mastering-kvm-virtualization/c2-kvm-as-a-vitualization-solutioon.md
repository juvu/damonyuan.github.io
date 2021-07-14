# C2. KVM as a Virtualization Solution

## Virtualization as a Concept

- multi-core
- additional CPU registers that can handle specific types of operations

Requirements,

- Hardware
- Software
  - protection rings
  - hypervisor or VMM runs in ring 0
  - the virtual machine's OS must reside in ring 1
  - virtualization methods
    - full virtualization (virtualbox)
      - priviledged instructions are emulated
      - `lscpu | grep Virtualization` -> it should show "Virtualization type: full"
    - paravirtualization
    - hardware-assisted virtualization (kvm)
      - new instructions
      - ring -1

## The Internal Workings of libvirt, QEMU and KVM

- libvirt -> API & daemon & managemnet tool for different types of hypervisors (libvirtd), connected to underlying hypervisor - QEMU / KVM
- libvirt client support drivers - primary and secondary drivers
  - Xen
  - Open VZ
  - QEMU
  - VirtualBox
  - Remote
  - Test
  - ...
- libvirt spawn the QEMU-KVM process and QEMU talks to the KVM kernel modules. In short, QEMU talks to KVM via different ioctl() to the /dev/kvm device file exposed by the KVM kernel module.
- virsh - <network> -> libvirt client - <AF_UNIX socket> -> libvirtd -> drivers, eg., QEMU - <ioctl /dev/kvm> -> vm
- check whether it's possible to start kvm:
  ```
  # when I say hardware-accelerated virtualization, I am mainly referring to Intel VT-X and AMD-Vs SVM
  lscpu | grep Virtualization
  Virtualization: VT-x
  ```

- QEMU can act as an emulator or virtualizer
  - QEMU AS AN EMULATOR:  Tiny Code Generator (TCG); it's a Just-in-Time (JIT) compiler
  - QEMU as a virtualizer: ioctl() -> /dev/kvm
- the physical RAM of the guest is inside the QEMU process address space

## How all these communicate with each other to provide virtualization
