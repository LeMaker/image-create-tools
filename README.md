The [LeMaker Guitar](http://www.lemaker.org/article-46-1.html) can boot system from the two different medium which include EMMC and SD card. In order to make the EMMC system image(.fw) easy, we provide the package tool, you can use the tool to make system image for EMMC quickly.
If you want to make system image for SD card, please refer to the LeMaker wiki at <http://wiki.lemaker.org/LeMaker_Guitar:How_to_make_LeMaker_Guitar_OS_image>

## Usage
	make-linux-emmc-fw --hwpack xxx_hwpack.tar.[xz|bz2|gz] --rootfs xxx_directory <--cfg xxx/partition.conf> <--output s500_lemaker_guitar>

## Command Options
	-g --cfg     Configure partition of the system image
	-p --hwpack  Choose platform firmware compression package
	-r --rootfs  Specify file system directory
	-h --help    Help information
	-c --clean   Clean all object file
	-o --output  Configure output file name

## Add New Partition
The tool create two partitions by default, if you want to add new partition to the system firmware, please add new node to the **config/partition.conf** according to the format below:

	[partition]
	label        = MISC                     ; label of the partition
	fstype       = EXT4/FAT16/FAT32/RAW     ; file system type of the partition
	size         = 48                       ; capacity of the partition(unit:MB), 0:empty partition -1: spare space of disk
	flag         = 0x01                     ; bit0=1: capacity of the partition equal to the image size  bit0=0: capacity of the partition equal to the parameter {size}, Other bits reserved
	downloadfile = xxx.img/FMT              ; name of the download image file(eg: misc.img rootfs.img), If there is no corresponding image file, you have to set the parameter with "FMT"

If you want to initialize the parition with image file, please refer to the following method to create an image file in advance:   

	1. sudo dd if=/dev/zero of={downloadfile} bs=1M count={size}     
	2. sudo mkfs.{fstype} -F -L {label} {downloadfile}  
	3. sudo mount -o loop {downloadfile}  /mnt  
	4. sudo cp -a "files" /mnt  
	5. sudo sync && umount /mnt  
Then copy the *{downloadfile}* to the **images** directory(be created automatically when using tool for the fist time), and start to make system firmware.

For more information about the configure file, please check **config/partition.conf**

## Attention
These system image (.fw for EMMC) are created by this tool only devided to two
partition (one is fat format, the other is ext4 format) by default and it can be burned to
**4G** or even larger EMMC.
If you want to expand the root file system when Linux OS is running, please refer
to the wiki at <http://wiki.lemaker.org/LeMaker_Guitar:How_to_resize_system_partition>

## Feedback and Improvements
If you meet some bugs, you can fix it and feel free to contribute your code to the Repository. Of course, you can also report bugs to <http://bugs.lemaker.org/>
