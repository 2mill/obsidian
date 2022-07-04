# fdisk
`fidsk <disk>` brings up the dialog for interacting with a block device that requires a partition.

When in a dialog with a device, you can use the following inputs:
`p` will print the current table.
`d` will delete the current existing partition.
`n` will allow for the creation of a new partition.
	`p` for primary.
		If primary, then you can choose primary number.
	`e` for extended.
	Both these options will be followed by partition sector and size.
`w` will write the changes to the disk.

