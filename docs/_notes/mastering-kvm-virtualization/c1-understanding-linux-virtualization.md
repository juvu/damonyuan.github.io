# C1 - Understanding Linux Virtualization

## Linux Virtualization and Its Basic Concepts

Different technologies,
- Red Hat with KVM
- Microsoft with Hyper-V
- VMware with ESXi
- Oracle with Oracle VM

## Types of Virtualization

Based on What,

- VDI
- Server Virtualization
- Application Virtualization
- Network Virtualization
- Storage Virtualization

Based on How,

- Partitioning
- Full Virtualization
  - Software-based (uses binary translation to virtualize the execution of sensitive instruction set)
  - Hardware-based (KVM / other popular hypervisors, such as ESXi, Hyper-V and Xen)
- Paravirtualization (no CPU virtualization extensions required)
- Hybrid Virtualization
- Container-based Virtualization (docker and podman, hypervisor + namspace + cgroup)

## Hypervisor / VMM

- type 1
- type 2

## Open Source Virtualization Projects

- KVM
- VirtualBox
- Xen
  - Xen hypervisor
  - Domo (Qemu)
  - management utilities
  - Virtual machines
- Lguest
- UML
- Linux-VServer

## What Linux Virtualization offers you in the Cloud

IaaS solutions,

- OpenStack (KVM)
- CloudStack (Xen)
- Eucalyptus (AWS, both KVM and Xen)