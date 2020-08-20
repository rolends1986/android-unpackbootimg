unpackbootimg
=============

unpackbootimg & mkbootimg to work with Android boot images.

Since image tools are not part of Android SDK, this standalone port of AOSP system/core aims to avoid complex building chains.

```
$ make
$ ./unpackbootimg
usage: unpackbootimg
  -i|--input boot.img
  [ -o|--output output_directory]
  [ -p|--pagesize <size-in-hexadecimal> ]
$ ./mkbootimg
usage: mkbootimg
       --kernel <filename>
       [ --ramdisk <filename> ]
       [ --second <2ndbootloader-filename> ]
       [ --cmdline <kernel-commandline> ]
       [ --board <boardname> ]
       [ --base <address> ]
       [ --pagesize <pagesize> ]
       [ --dt <filename> ]
       [ --kernel_offset <base offset> ]
       [ --ramdisk_offset <base offset> ]
       [ --second_offset <base offset> ]
       [ --tags_offset <base offset> ]
       [ --os_version <A.B.C version> ]
       [ --os_patch_level <YYYY-MM-DD date> ]
       [ --hash <sha1(default)|sha256> ]
       [ --id ]
       -o|--output <filename>
$ ./mkbootimg.py
usage: mkbootimg.py [-h] --kernel KERNEL [--ramdisk RAMDISK] [--second SECOND]
                    [--cmdline CMDLINE] [--base BASE]
                    [--kernel_offset KERNEL_OFFSET]
                    [--ramdisk_offset RAMDISK_OFFSET]
                    [--second_offset SECOND_OFFSET] [--os_version OS_VERSION]
                    [--os_patch_level OS_PATCH_LEVEL]
                    [--tags_offset TAGS_OFFSET] [--board BOARD]
                    [--pagesize {2048,4096,8192,16384}] [--id] -o OUTPUT
```

Credits to [@osm0sis](https://github.com/osm0sis/mkbootimg) for maintaining
most of the unpackbootimg logic that is no longer present in AOSP.

mac os build 
 
export CC=gcc -m64 \
export LD=ggcc \
export DEP_CC=gcc
make

./aarch64-dump  -EL -b binary -D -m armv5t  ./arm-linux-4.9.18.zImage  | grep 8b1f
       0:	00088b1f 	andeq	r8, r8, pc, lsl fp
dd if=./KERNEL.img-zImage of=piggy.gz bs=1 skip=0

/home/ching/Android/Sdk/ndk-bundle/toolchains/aarch64-linux-android-4.9/prebuilt/linux-x86_64/bin/aarch64-linux-android-objdump -EL -b binary -D -m armv5t  ./kernel.img-zImage.vmlinux
===============
./unpackbootimg -i ./kernel.img
//如果需要代理先要sudo su root接着export   https_proxy="127.0.0.1:1089"
sudo python3 -m pip install --upgrade lz4 git+https://github.com/marin-m/vmlinux-to-elf

 
 //解包后可以导
 objdump -EL -b binary -D -m armv5t  ./kernel.img-zImage.vmlinux | grep memstart_addr
 vmlinux-to-elf  ./kernel.img-zImage   ./kernel.elf
readelf -s ./kernel.elf | grep memstart_addr


