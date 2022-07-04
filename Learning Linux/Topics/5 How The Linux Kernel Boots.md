# How the Linux Kernel Boots

## Startup Messages
The kernel spits out information about its boot process, but these can go buy quickly with how fast boot times are these days.
To view the kernel system log, visit `/var/log/kern.log`
`dmesg` is a command that can be used to view these messages as well.
When it comes to startup scripts, those are usually maintained by the service.

 ## Kernel Initialization and Boot Options
 The kernel runs through the following steps:
 1. CPU inspection
	 Nothing much impressive, or to be concerned about.
 2. Memory Inspection
 3. Device bus discovery
 	The kernel would need to have the right drivers for these device buses.
 1. Device discovery
 	These devices might not be found, if there is no proper bus drivers.
 1. Auxiliary kernel subsystem setup(networking, etc.)
 2. Root filesystem mount
 	At this point the root filesystem is mounted at `/`.
 1. User space start
 	The kernel will memory protect itself and start the first user space program.
 
 
 ## Kernel Parameters
 
I still don't quite get this part.

## Boot Loaders
Boot loaders help place the kernel into memory, provide crucial drivers, and pass kernel parameters. 

The boot loader uses the drivers contained within the BIOS or UEFI system that is hard coded to the motherboard.

using `efibootmgr` will help determine if your motherboard using UEFI or not.
You can also check `/sys/efi` if the folder exists or not.

### Boot Loader Tasks

The goal of a boot loader is to:
+ Allow for the selection of multiple kernels.
+ Create kernel parameters for each kernel.
+ Allow for the booting of other operating systems.
+ allow for the editing of kernel image names.

### Boot Loaders overview
+ [[GRUB]] the most used.
+ LILO
+ SYSLINUX
+ LOADLIN
+ systemd-boot
+ coreboot
+ Linux Kernel EFISTUB
+ efilinux
	Boot loader for EFI systems, used a template for others to support EFI.
	
# GRUB
For more information regarding GRUB, please visit [[GRUB]]