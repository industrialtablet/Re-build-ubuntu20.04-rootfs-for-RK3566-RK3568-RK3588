# Re-build-ubuntu20.04-rootfs-for-RK3566-RK3568-RK3588
This repository is the documentation for RK3566 RK3568 RK3588 products, written by RSD Team of HYY Technology Co.,Ltd.



1. Create new image file.

   ```shell
   dd if=/dev/zero of=ubuntu_rootfs.img bs=1M count=4096 		#size=4096MB
   ```

2. Formate the image file to ext4 file system.

   ```shell
   mkfs.ext4 ubuntu_rootfs.img
   ```

3. Mount the empty image file to ubuntu_new_rootfs fold.

   ```shell
   mkdir ubuntu_new_rootfs
   sudo mount ubuntu_rootfs.img ubuntu_new_rootfs
   ```

4. Mount the old image file to ubuntu_rootfs fold.

   ```shell
   mkdir ubuntu_old_rootfs
   sudo mount ubuntu_rootfs.img ubuntu_old_rootfs
   ```

5. Copy all old files to ubuntu_new_rootfs fold.

   ```shell
   sudo cp -rfp ubuntu_rootfs/* ubuntu_new_rootfs/
   ```

6. Run new file systme on virtual machine.

   ````shell
   bash mount.sh -m ubuntu_new_rootfs/
   root@admin:/#
   ````

7. install new softwares and exit the visual machine.

   ````shell
   root@admin:/#dpkg -i xxxxx.deb
   root@admin:/#exit
   ````

8. umount the images.

   ````shell
   bash mount.sh -u ubuntu_new_rootfs/
   sudo umount ubuntu_new_rootfs/
   sudo umount ubuntu_old_rootfs/
   ````

9. check and resize new rootfs.

   ````shell
   e2fsck -p -f ubuntu_rootfs.img
   resize2fs -M ubuntu_rootfs.img
   ````

10. Sovle build firmware error with  "rk356x_ubuntu_rootfs.img's size exceed parameter.txt's limit! "

    Modify file device/rockchip/rk356x$ vim parameter-ubuntu-fit.txt

    rootfs partition:  	

    [partitition size]@[start address], userdate partition's start address is (rootfs start address + rootfs size)

    uboot partition example: 

    0x00002000 *512byte = 8192 * 512byte = 4,194,304byte 4,194,304÷1024 = 4096KB  4096÷1024=4MB  So uboot size is 4M



## Get More technical Support

###### RK3588 Development Board

\- [RK3588 Development Board](https://github.com/industrialtablet/RK3588-Development-Board)

###### ota upgrade tools(otaStar) and server

\- [RK3566/RK3568/RK3588 Android OTA upgrade tools and server](https://github.com/tablet-pc/otastar)

###### How Qt5.14.2 cross-compile

\- [RK3588 Qt5.14.2 cross-compile for Ubuntu and Debian Linux OS](https://github.com/pengyixing/qt-everywhere-src-5.14.2-cross-compile-for-RK3566-RK3568-RK3588)

Build Videorecorder Bundle use Networkoptix Client on HYY H-3588 Tablet

\- [Build Videorecorder Bundle use Networkoptix Client](https://github.com/industrialtablet/Build-Videorecorder-Bundle-use-Networkoptix-Client-on-HYY-RK3566-Tablet)



# Contacts

- Website: www.we-signage.com
- https://we-signage.en.made-in-china.com/
- E-mail: dennis@we-signage.com
- MP/Whatsapp/Wechat: + 86 13349909990
- Skype: solled686
