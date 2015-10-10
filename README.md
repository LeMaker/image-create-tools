The [LeMaker Guitar](http://www.lemaker.org/article-46-1.html) can boot system from the two different medium which include EMMC and SD card.
In order to make the EMMC system image(.fw) and SD system image(.img) easy, we provide the package tool, you can use the tool to make system
image quickly.

## Usage
	linux-image-create --type [emmc|sd] --hwpack xxx_hwpack.tar.[xz|bz2|gz] --rootfs xxxx_rootfs.tar[.bz2|xz|gz] <--output s500_lemaker_guitar>

## Command Options
        -t --type    Configure image type
        -p --hwpack  Chose platform firmware compression package
        -r --rootfs  Chose root file system
        -h --help    Help information
        -c --clean   Clean all object file
        -o --output  Configure output file name

## Attention
These system image (.fw for EMMC and .img for SD card) are created by this tool
only devided to two partition (one is fat format, the other is ext4 format) and it 
can be burned to **4G** or even larger SD/EMMC card.
If you want to expand the root file system when Linux OS is running, please refer
to the wiki at <http://wiki.lemaker.org/LeMaker_Guitar:How_to_resize_system_partition>

## Feedback and Improvements
If you meet some bugs or have improving suggestions about the tool, please contact us by the email <support@lemaker.org>
