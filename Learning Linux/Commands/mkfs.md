# mkfs
`mkfs` allows for the creation of filesystems on paritioned block devices.
To read more about the various filesystems that can be used, refer to [[filesystems]].

Keep in mind that creating a new filesystem ontop of already existing data will more than likely wipe the old data.

### examples
`mkfs -t ext4 /dev/sda1` -t followed by an option will specify the filesystem type.
`mkfs -n device` can reprint the superblock backup number.
