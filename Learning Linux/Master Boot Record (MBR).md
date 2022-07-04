MBR is listed as `msdos` when looked at through `parted -l`'s commnad.
MBR will not have a column for naming partitions unliked GPT.

MBR can have four primary partitions and one swap.
If you want more partitions after the first four primary, extended partitions need to be created and are designated with `ext2/3/4`.
