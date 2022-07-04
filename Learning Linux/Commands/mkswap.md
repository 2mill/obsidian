# `mkswp`

## The Basics
`mkswap` creates a swap parition.
`swapon` places that new swap partition on the kernel registry.
`swapoff` removes that device from the swap registry.

## Making swap spaces on devices
`mkswap dev` designate a partition as the swap space.
`swapon dev` will register the swap space with the kernel.
Afterwards, make sure that you write swap entry into `/etc/fstab`
[[fstab]]

## Making swap spaces on files
Because devices are abstracted with files, it is also possible to designate a file with block size as a swap space.
`dd if=/dev/zero of=swap_file bs=1024k count=num_mb`
```sh
dd if=/dev/zero of=swap_file bs=1024k count=num_b
mkswap swap_file
swapon swap_file
```

because `/dev/zero` is a continuous stream of characters, count must be set.
