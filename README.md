This is a guide for install MacOSX on Dell 7559 Laptop
=
In this guide, all operation take my Dell 7559 as exmaple, APCI files(SSDT and APCI fixed in clover may not compatible with your hardware, be careful to using them, repatch in need).
 --- 
  1. CPU: i5-6300HQ (Skylake,6th)      Mem:  4G DDR3, in one slot
  2. Graphic: Intel HD Graph 530 + Nvida GTX960M
  3. Display: 1920x1080 FHD screen     Disk: 128G SSD + 500G HDD
### Before Start：
    1. There's something must noticed:
        A. The i7 edition is easy to make Hackintosh
        B. The i5 editon is hard to boot frome UEFI Clover
    2. There's Something you must have and keep for long time on you Hackintosh way
        A. noun  B. patience  C. time  D. learning skill

 Prepare:
 -
 #### Understand your hareware:
  Have a look into Laptop Guide from manufacturer<br>
  Check hardware on the normal running Operation Systme（Windows/linux，etc.）<br>
  List and record hardware details
  #### Download files:
Get an working Mac OSX and download installer image from Mac app stroe<br>
##### Create bootable USB installer with Clover follow this [thread](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/).<br>

Ensure and format usb disk into GPT disk, operate in terminal:
-
>crackselfs-MBP:~ crackself$ diskutil list<br>
>>/dev/disk0 (internal, physical):<br>
-
 >>>#:       TYPE NAME\                                     SIZE       IDENTIFIER<br>
 >>>0:       GUID_partition_scheme                        *128.0 GB  disk0<br><br>
 >>>1:                        EFI EFI                     209.7 MB   disk0s1<br>
 >>>2:         Microsoft Reserved                         16.8 MB    disk0s2<br>
 >>>3:       Microsoft Basic Data Windows                 63.8 GB    disk0s3<br>
 >>>4:                  Apple_HFS Mac                     63.3 GB    disk0s4<br>
 >>>5:                 Apple_Boot Recovery HD             650.0 MB   disk0s5<br>
 
>>/dev/disk2 (external, physical):<br>
-
 >>>#:                       TYPE NAME                     SIZE      IDENTIFIER<br>
 >>>0:       GUID_partition_scheme                        *15.6 GB   disk2<br>
 >>>1:                        EFI EFI                     209.7 MB   disk2s1<br>
 >>>2:       Microsoft Basic Data                         15.2 GB    disk2s2\<br>
 
as the result, /dev/disk2 is the usb disk.<br>
Format it as one GPT partiton whit EFI partiton:
diskutil partitionDisk /dev/disk2 1 GPT HFS+J "install_osx" R

then, write installer inamge into usbdisk
For Hight Sierra(10.13.x):
sudo "/Applications/Install macOS High Sierra.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --nointeraction
For Sierra(10.12.x)
sudo "/Applications/Install macOS Sierra.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --applicationpath "/Applications/Install macOS Sierra.app" --nointeraction
For El Capitan(10.11.x)
sudo "/Applications/Install OS X El Capitan.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --applicationpath "/Applications/Install OS X El Capitan.app" --nointeraction
After finish, rename usb disk as install_osx
Noticed: Dell 7559 with Skylake cpu, OS support from 10.11

## Install Clover into usb EFI partition:
here suggest using origin installer(https://sourceforge.net/projects/cloverefiboot/)

For UEFI boot:
check all this:
  Only install UEFI
  Theme
    BGM
  install in EFI partition
  Drivers64UEFI
      AptioMemoryFix

For UEFI and legacy clover boot:
  install in EFI partition
  Theme
    BGM
  Bootloader
    Bios boot0af
  CloverEFI
    CloverEFI 64bit BiosBlockIO
  Drivers64UEFI
    AptioMemoryFix

Noticed: as UEFI/legacy clover Boot model suggeste for i5 EDITON.
After install fiish, replace universal config.plist files frome RehabMan; place must kexts into Clover/Kext/Ohters

Postinstall:
One step need to explain:
install clover into SSD HDD EFI partiton as well as operate on installer,but check install RCscripts in target partiton, This afect store your backlight leverl.

Others:
Using my Clover files to test, if your hardware do not work perfect, Repatch your APCI files and check kexts, in additon, RehabMan suggest Kest install into L/E, rebuild kextcache wiht comandline "sudo kextcache -i /".

Get hardware work normally:
Graphic
Audio:
Wi-Fi card
Ethernet
Keyboard and mouse
Power Manager(Sleep and wake )
