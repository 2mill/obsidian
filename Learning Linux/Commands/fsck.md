# `fsck`
`fsck` can help check a block device's filesystem for corruption.

!!! WARNING
Do not use this while the system is mounted. The only times you should be using this command is if the mounted filesystem is read-only and in single user mode. Doing so otherwise can fuck shit up badly.


`fsck /dev/sda1` is an example of fsck checking the first parition on the device `/dev/sda1`.
The program will prompt if things have happened such as lost inodes etc.

`lost+found` is the file that `fsck` will dump disconnecred *inodes* into.

`fsck -p` will automatically go through common problems and fix them.
`fsck -n` will find what's wrong without writing any changes.
`fsck -b *num*` is to be used if the superblock is fucked and you have a backup number for the superblock that [[mkfs]] dumps.

