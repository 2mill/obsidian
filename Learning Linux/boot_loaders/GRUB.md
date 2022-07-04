# GRUB
Can be accessed by holding SHIFT or ESC during the BIOS splash screen.

To view the boot loader configuration, press `e`.

Pressing `c` from the splash menu will open the GRUB command line.
### Grub Command Line
#### Listing Devices
This section should be filled out later.
#### File Navigation
This section needs to be filled out later after some practice.

	

You will see a list of commands listed in the grub boot config, and will more than likely need to google them.


## Grub Configuration
`grub.cfg` can be found in `/boot/grub(2+)`.
Variables start with a `$` and cna be found in a `load_env` file.

The first lines will be setup commands for values, functions, and graphics settings.

the boot configurations are contained in within `menuentry ... {}`


### Generating New Configuration Files
New configuration files are to be made within a separate file followed by the usage of the command `grub-mkconfig`.

To make your own custom grub configurations, it is advised to be placed in `/boot/grub/custom.cfg`.
	At this point 

