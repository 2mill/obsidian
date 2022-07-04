# mount

`$mount` is the command for mount.
Doing just `mount` will print out the list of devices that are mounted and where they are mounted at.
```
bridge@Yannicks-MacBook-Pro ~ % mount
/dev/disk1s6s1 on / (apfs, sealed, local, read-only, journaled)
devfs on /dev (devfs, local, nobrowse)
/dev/disk1s4 on /System/Volumes/VM (apfs, local, noexec, journaled, noatime, nobrowse)
/dev/disk1s2 on /System/Volumes/Preboot (apfs, local, journaled, nobrowse)
/dev/disk1s7 on /System/Volumes/Update (apfs, local, journaled, nobrowse)
/dev/disk1s1 on /System/Volumes/Data (apfs, local, journaled, nobrowse)
/dev/disk1s5 on /Volumes/Macintosh HD - Data (apfs, local, journaled)
map auto_home on /System/Volumes/Data/home (autofs, automounted, nobrowse)
/dev/disk2s1 on /Volumes/KEYDRIVE (msdos, local, nodev, nosuid, noowners)
```

There will be the device, the mount point for the device and extra mount options.

An example of a mount command would be the following
`mount -t type device mountpoint`
`mount -t ex4 /dev/sdf2 /home/extra`
	`-t` defines the filesystem for `/dev/sdf2` to be the Extended Filesystem 4
	`-t` is optional, because mount should figure out what the filesystem is.
`umount` unmounts devices.

`mount UUID mountpoint` also works as a designator and more ironclad than just using the device name.

## Mount options
There are a lot of mount options, and are covered in better extent in mount(8)

There are short hand options such as
`-r` mounts as read only.
`-n` does not write to `/etc/mtab` which mount needs to do or else it fails. Also good for debugging in single user mode.
`-t` type as explained before
### Long Options
Short options are good, but not easy to read. Appending `-o` gives access to a line of options
For example: `mount -t /dev/sde1 /dos -o ro,uid=1000`


### Remounting a Filesystem
If you need to remount a filesystem for various reasons, you can use `-o remount`
`mount -n -o remount mountpoint`
	`-n` is in the command, because sometimes you will need to remount when `/etc/mtab` is in read only mode.