# Disks and Filesystems
Linux disk devices are represented with labelings such as `/dev/sda`.

These disks will be subdivided to provide a filesystem structure.

The file system structure will consist of the following eliments.

-   Partition Table
-   Partition
    -   Filesystem Data Structure
        -   This is the file system and is interacted with on the user level.
    -   File Data
        -   This is all of the data that is contained within your file system.
-   Partition(if there is another one on the same disk).
    -   There might be extra file partitions located on a device and are marked by higher incremented sda such as `sda2` or `sda3` etc.
    -   These extra partition might be present for swap partitions, or reserving some system space for actual system processes.

The Linux kernel allows for the access of multiple partitions, but there is no real reason for doing this, and LVM systems are better equipped at automatically handling this for you.

It is possible to work with disks directly through the filesystem as well as manipulating the disk device directly.

## Partitioning Disk Devices

When making partitions on a disk, there are different standards, and different tools that can be used for partioning.

The most common disk partition tables are:

-   [[Master Boot Record (MBR)]]
    
    MBR, when listed with `parted -l` will have columns for size, flags and other things, but no name. GPT will have a name.
    
    `parted -l` will display MBR as `msdos`.
    
-   Globally Unique Partition Table(GPT)
    

and the most popular tools used for generating these tables are:

-   parted (’partition editor’)
    -   text based, supports MBR and GPT. Simpler to use if you know what you are doing.
    -   However, dangerous in the hands of an inexperienced user.
-   gparted
    -   Graphical version of parted.
-   fdisk
    -   Preferred, because it won’t write the table until the user has verified.
    -   Should orient to using this tool more often.

Using `parted -l` will display your disk devices, partition table(either MBR or GPT), and what partitions exist.

When looking at `parted -l` output, parted will demarkate MBR as `msdos`.
### Modifying Partition Tables
More information on this can be found in [[fdisk]]
## Filesystems
There are several filesystems out there and all of them do things better than others for various reasons. Read more about filesystems at [[filesystems]]

If you have chosen a filesystem and are ready to implement, go ahead and use the [[mkfs]] command to write a new file system to a partition that you have made.

## Mounting a Filesystem
The main command used for mounting files is [[mount]]

Filesystems are to be mounted on a point after your kernel mounts root on `/`.

### Filesystem UUID
Device names can change, because of the way the Linux kernel discovers devices.

To ensure that the kernel always mounts the correct device, you can use the Universally Unique Identifier(UUID).

[[blkid]] is a tool for listing all of the block devices and their corresponding IDs as well as information regarding the filesystem type.


### Disk Buffering and Caching Filesystems
The kernel waits for the right time to make changes to the disk.
`sync` forces the kernel to make changes to the disk and should be done before unmounting a disk.
The kernel also keeps a cache of recently retrieved disk data.

### The `/etc/fstab` Filesystem Table
If you want the kernel to mount on boot, make expression in /etc/fstab with either the device name or UUID, mountpoint, filesystem type, options.
![[Pasted image 20220531233313.png]]

The first of the last two digits do not matter and should always be set to 0.
The last number depends.
	`1` for the root filesystem
	`2` for any other filesystems on the disk
	`0` for disabling the bootup check, and should be used for read only devices
	
There are some extra options that are not present in mount
	`defaults`
		gives rw, setuid bit etc to default values. Fills in the blanks.
	`errors`
		`errors=continue` if the filesystem fails to mount to have the system keep running
		`errors=remount-ro` attempt to remount in ro
		`errors=panic` panic the system if it fails to mount
	`user`
		Used for allowing users to mount on particular entries. Gives other devices `nodev`, `noexec` and `nosuid`
	`noauto`
		Tells `mount -a` to ignore auto mounting the filesystem.
		
#### Alternatives to `/etc/fstab`
You can use `/etc/fstab.d` which contains individual files for each mount configuration.
`systemd` but this part will be fleshed out more later.
### Filesystem Capacity
[[df]] will show you disk usage.

### Checking and Repairing Filesystems
If you happen to shutdown the computer abruptly while the kernel and block device is out of sync [[fsck]] will help with fixing things. 

There are various other filesystem checking algorithms particular for each filesystem, but `fsck` will figure out what program it should be using.
### Special-Purpose Filesystems
`proc` mounted at `/proc`
	Directories represent processes, and are represented with their process ID.
	`/proc/self` is the current running process.
	
`sysfs` mounted on /sys
`tmpfs` used to represent your system memory and swap space. `tmpfs` can be mounted anywhere, but dumping data into it can fill up memory too quickly.
`squashfs` A filesystem that keeps files compressed in a read only format.
`overlay` a file system that merges direcotires into a composite.
## The Swap Space
Swap spaces augment the functions of RAM, but on the disk.
The make a swap space, use the command [[mkswap]].

### Determining How much swap space
Make a little swap space but not too much. If both the RAM and swap space are filled up, the Linux kernel will begin killing random processes.

## The Logical Volume Manager
The logical volume manager allows for the addition of storage without needing to assign filesystems, or new partitions. 

LVMs are possible through a Volume manager that links physical volumes to logical volumes. 

Devices within a logic group are capable of being removed, added to, or resized depending on the needs.
### Working with LVMs
To work with LVMs, you will need to use the [[lvm]] command.

### Using Logical Volume Devices
Logical volumes can be found at `/dev/dm-0`, `/dev/dm-1` etc. These are not reliable references, and therefore using a symlink established is better.

The LVM will make sym links for these logical volumes in `/dev/mapping`

## Looking Forward: Disks and User Space

### Inside a Traditional Filesystem

There are two components of a filesystem.
	A pool of data.
	A database holding all of the inode data.
*inodes* point towards data pools, the amount of inodes pointing to it and the inode type(file/directory).
	You can view inodes by using the `stat` command on a file or directory.
	
### Block Allocation
The kernel maintains a check on what blocks are allocated and which ones are available. When a filesystem is removed without syncing this data, this sync can fall out of sync.

If these are out of sync, `fsck` will attempt to fix it. Any inodes that are lost during this process are placed into `lost+found`

When inodes in `lost+found`, it is up to the user to figure out what the purpose of these files are.
### Working with Filesystems in User Space
Working with inodes should be the least of your concerns. 
Some filesystems do not have inodes at all, but are presented as such due to the VFS.

