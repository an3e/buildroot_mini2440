buildroot_mini2440
==================

contains a buildroot based project for mini2440 development board

Boot options
============

1 Booting from NFS
~~~~~~~~~~~~~~~~~~
1.1 bootargs
console=ttySAC0,115200 noinitrd consoleblank=0 mini2440-nand root=/dev/nfs rw nfsroot=10.175.196.221:root=/dev/nfs rw nfsroot=10.175.196.221:/srv/nfs
1.2 bootcmd
nfs 0x32000000 10.175.196.221:/srv/nfs/boot/uImage; bootm

2 Booting from SD Card
~~~~~~~~~~~~~~~~~~~~~~
2.1 bootargs
console=ttySAC0,115200 mini2440=3tb rootfstype=ext3 root=/dev/mmcblk0p3 rw rootwait
2.2 bootcmd
mmcinit; ext2load mmc 0:1 0x32000000 uImage; bootm 0x32000000

SD card contains 3 partitions:
	- first partition has ext2 filesystem and contains uImage
	- second partition is swap partition
	- third partition has ext3 filesystem and contains rootfs
