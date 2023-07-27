## Virtualization

#### Running Virtual Machines on RHEL

### Objectives:

At the end of this episode, I will be able to:

1. Differentiate between QEMU, KVM, and libvirt.
2. Describe the hardware requirements for virtualization.
3. Install and configure QEMU, KVM, and libvirt.
4. Create a virtual machine and connect to its console for management.

`sudo dnf install qemu-kvm qemu-img libvirt virt-manager`

`sudo systemctl enable --now libvirtd`

`sudo systemctl status libvirtd`

![[Pasted image 20220613031704.png]]

`sudo dnf install virt-install`
![[Pasted image 20220613032210.png]]

![[Pasted image 20220613032244.png]]

`/var/lib/libvirt`- This is where alot of our stuff resides - like iso images and dsk images.
