# OpenWrt Filesystem Compression

[make run output log](refer/runlog)

## gz tar command

`tar -cp --numeric-owner --owner=0 --group=0 --sort=name --mtime="@1508262380" -C /home/zengjf/openwrt-17.01.4/build_dir/target-arm_cortex-a9+neon_musl-1.1.16_eabi/root-imx6/ . | gzip -9n > /home/zengjf/openwrt-17.01.4/bin/targets/imx6/generic/lede-imx6-generic-rootfs.tar.gz`

### Analysis tar command

* -c: create a new archive
* -p: extract information about file permissions
* --numeric-owner: always use numbers for user/group names 
* --owner=0: force NAME as owner for added files
* --group=0: force NAME as group for added files
* --sort=ORDER: Specify the directory sorting order when reading directories. ORDER may be one of the following:
  * name: Sort the directory entries on name. The operating system may deliver directory entries in a more or less random order, and sorting them makes archive creation reproducible.
* --mtime=date: When adding files to an archive, tar will use date as the modification time of members when creating archives, instead of their actual modification times. 
* -C: --directory DIR, change to directory DIR

### Analysis gzip command

* -# --fast --best  
  Regulate the speed of compression using the specified digit #, where -1 or --fast indicates the fastest compression method  (less  compression)  and  -9 or --best indicates the slowest compression method (best compression).  The default compression level is -6 (that is, biased towards high compression at expense of speed).
* -n --no-name  
  When  compressing,  do  not save the original file name and time stamp by default. (The original name is always saved if the name had to be truncated.) When decompressing, do not restore the original file name if present (remove only the gzip  suffix  from  the  compressed  file name) and do not restore the original time stamp if present (copy it from the compressed file). This option is the default when decompressing.

## Buildroot bz2 tar command

`PATH="/home/zengjf/zengjf/Buildroot/buildroot/output/host/bin:/home/zengjf/zengjf/Buildroot/buildroot/output/host/sbin:/home/zengjf/zengjf/Buildroot/buildroot/output/host/usr/bin:/home/zengjf/zengjf/Buildroot/buildroot/output/host/usr/sbin:/home/zengjf/zengjf/buildroot-2017.02.3/output/host/usr/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games" bzip2 -9 -c /home/zengjf/zengjf/Buildroot/buildroot/output/images/rootfs.tar > /home/zengjf/zengjf/Buildroot/buildroot/output/images/rootfs.tar.bz2`

### Analysis bzip2 command

* -1 (or --fast) to -9 (or --best)  
  Set the block size to 100 k, 200 k ... 900 k when compressing. Has no effect when decompressing. See MEMORY MANAGEMENT below. The --fast and --best aliases are primarily for GNU gzip compatibility. In particular, --fast doesn't make things significantly faster. And --best merely selects the default behaviour.
* -c --stdout  
  Compress or decompress to standard output.

## Grep Filesystem

```
zengjf@desk-ubuntu:~/openwrt-17.01.4$ grep CONFIG_TARGET_ROOTFS_TARGZ * -R
...
config/Config-images.in:        config TARGET_ROOTFS_TARGZ
include/image.mk:ifdef CONFIG_TARGET_ROOTFS_TARGZ
...
tmp/.diffconfig.stage1.old:CONFIG_TARGET_ROOTFS_TARGZ=y
tmp/.config.old:CONFIG_TARGET_ROOTFS_TARGZ=y
tmp/.diffconfig.stage2.old:CONFIG_TARGET_ROOTFS_TARGZ=y
tmp/.config:CONFIG_TARGET_ROOTFS_TARGZ=y
tmp/.diffconfig.stage1:CONFIG_TARGET_ROOTFS_TARGZ=y
tmp/.diffconfig.stage2:CONFIG_TARGET_ROOTFS_TARGZ=y
zengjf@desk-ubuntu:~/openwrt-17.01.4$
```

### Source Code

```
zengjf@desk-ubuntu:~/openwrt-17.01.4$ cat include/image.mk
...
ifdef CONFIG_TARGET_ROOTFS_TARGZ
  define Image/Build/targz
        $(TAR) -cp --numeric-owner --owner=0 --group=0 --sort=name \
                $(if $(SOURCE_DATE_EPOCH),--mtime="@$(SOURCE_DATE_EPOCH)") \
                -C $(TARGET_DIR)/ . | gzip -9n > $(BIN_DIR)/$(IMG_PREFIX)$(if $(PROFILE_SANITIZED),-$(PROFILE_SANITIZED))-rootfs.tar.gz
  endef
endif
...
```

### Config-images.in

https://git.openwrt.org/?p=openwrt/openwrt.git;a=blob;f=config/Config-images.in
