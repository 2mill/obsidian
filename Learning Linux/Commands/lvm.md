# `lvm`
The `lvm` command is started from the command prompt, followed by a dialog that allows for the management of lvms and other features of the lvm.

## Listing Volume Groups
`vgs` will list the current volume groups
	`vgs` will spit out information with various headers. The meaning for the headers are as follows:
		`VG`: Volume group name.
		`#PV`: The number of physical volumes the group has.
		`#LV`: The number of logical volumes within the group.
		`#SN`: The # of LVM snapshots
		`#Attr`: The things that are possible to do with this logic volume group
			`w` is writable
			`z` is resizable
			`n` 'normal allocation policy'
		`VSice`: The volume group size
		`VFree`: How much is left within the group
`vgsdisplay` is more detailed information about the volume groups.	
	`Open LV` the number of physical volumes in use.
	`Cur PV` The # of physical volumes within the group.
	`Act LV` How many active physical volumes 
	`VG UUID` The volume group UUID


## Listing Logic Volumes
`lvs` and `lvdisplay` will display the short and long list respectively.

For `lvs`, you will run into the following names:
	`LV` The logical volume name
	`VG` The volume group where this logical volume resides.
	`Attr` Attributes of the logical volume.
		`w` wiretable,
		`i` inherited allocation policy,
		`a` active,
		`o` open
	`LSize` the size of the logical volume.
	
## Listing Physical Volumes
`pvs` and `pvdisplay` displays the short and long list version respectively.
	
