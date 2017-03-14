## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution

Ok, we're given a backup.iso file. I first tried to mount the iso, and it wouldn't mount. Annoying. Let's see what we can figure out about it. If you've looked at the reversing section, you'll know the drill.

```
$ ls -alh
total 513024
drwxr-xr-x   3 #####  staff   102B Mar 13 20:33 ./
drwxr-xr-x  15 #####  staff   510B Mar 10 02:34 ../
-rw-r--r--@  1 #####  staff   251M Mar  9 15:13 backup.iso

$ file backup.iso
backup.iso: data
```
Ok... File didn't pick it up, and 251MBs is to large to look at it with xxd. Let's look at it with another tool.

The one I use here is [BinWalk](http://tools.kali.org/forensics/binwalk).
> Binwalk is a tool for searching a given binary image for embedded files and executable code. Specifically, it is designed for identifying files and code embedded inside of firmware images. Binwalk uses the libmagic library, so it is compatible with magic signatures created for the Unix file utility. Binwalk also includes a custom magic signature file which contains improved signatures for files that are commonly found in firmware images such as compressed/archived files, firmware headers, Linux kernels, bootloaders, filesystems, etc.

Basically, binwalk goes through the whole binary using libmagic same as `file`, except `file` only runs on the header while this tool searches throughout the whole file.

```
$ binwalk backup.iso

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
3392522       0x33C40A        MySQL ISAM compressed data file Version 7
21083031      0x141B397       LANCOM WWAN firmware
76748860      0x493183C       VMware4 disk image
158990032     0x979FED0       Zip archive data, at least v2.0 to extract, name: myThirdApp
158992638     0x97A08FE       End of Zip archive
164500682     0x9CE14CA       MySQL ISAM compressed data file Version 5
```

Good, we found some stuff. Let's extract it out.

```
$ binwalk -e backup.iso

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
3392522       0x33C40A        MySQL ISAM compressed data file Version 7
21083031      0x141B397       LANCOM WWAN firmware
76748860      0x493183C       VMware4 disk image
158990032     0x979FED0       Zip archive data, at least v2.0 to extract, name: myThirdApp
158992638     0x97A08FE       End of Zip archive
164500682     0x9CE14CA       MySQL ISAM compressed data file Version 5

$ ls
_backup.iso.extracted/ backup.iso

$ cd _backup.iso.extracted/

$ ls
979FED0.zip  myThirdApp*

$ file myThirdApp
myThirdApp: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=aafe6a0fc52383e25c88235220562efb550f9555, not stripped
```

Well, it's a linux executable; `ELF 64-bit`. I don't know an easy way to run this on a Mac, so let's move it over to a linux box and check it out.

```
$ scp myThirdApp root@kali:/tmp
root@kali's password:
myThirdApp                                                                        100% 7024     1.7MB/s   00:00

$ ssh root@kali
root@kali's password:

root@kali:$ cd /tmp/

root@kali:/tmp$ ./myThirdApp
flag: Password=DigitalForensicsIsEasyJustAskKali
```
Bingo! GAME OVER.

## Key
DigitalForensicsIsEasyJustAskKali
