# Comprehending Commands
## cat: not the pet, but the command 
cat is most often used for reading out files. In this challenge the flag is copied to the flag file in the home directory.
```
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{sEoWwC1C98Ig3S5AUzmNpJgTbt_.dFzN1QDLygDO0czW}
```
## catting absolute paths 
In this challenge the flag is stored in absolute path ```/flag```.
```
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{E36tqZaIrLSjM8L5fqeeraKYOqp.dlTM5QDLygDO0czW}
```
## more catting practice 
Similar logic just a different path 
```
You cannot use the 'cd' command in this level, and must retrieve the flag by 
absolute path. Plus, I hid the flag in a different directory! You can find it 
in the file /usr/libx32/gconv/flag. Go cat it out **without** cding into that 
directory!
```
In order to retrieve the flag we run 
```
hacker@commands~more-catting-practice:~$ cat /usr/libx32/gconv/flag
pwn.college{U5-ME-odkvsec62slK37FB-1he1.dBjM5QDLygDO0czW}
```
## grepping for a needle in a haystack 
In this challenge we are introduced to the grep command which is used to search for contents.
The syntax of the grep command 
```
hacker@dojo:~$ grep SEARCH_STRING /path/to/file
```
Here we are told that the flag is present in /challenge/data.txt file and we know that flags have the phrase pwn.college. Hence upon running the program as below we obtain the flag.

```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{oAZjzNtF3xomZtj9Phki6WWMtSE.ddTM4QDLygDO0czW}
```
## Listing files 
In this challenge we are intoduced to yet another command known as the ls command.
ls will list files in all the directories provided to it as arguments, and in the current directory.
In this challenge we are asked to list all the directories in ```/challenge```
```
hacker@commands~listing-files:/challenge$ ls /challenge
7542-renamed-run-16659  DESCRIPTION.md
hacker@commands~listing-files:/challenge$ /challenge/7542-renamed-run-16659 
Yahaha, you found me! Here is your flag:
pwn.college{g4_WtwMVa6QtY4iFp0XCI6tDcdt.dhjM4QDLygDO0czW}
```
## touching files 
We can create new blank files using the touch command.
The syntax or the command looks like so: ```hacker@dojo:/tmp$ touch filename```
In this level we need to create two files:```/tmp/pwn``` and ```/tmp/college```, and run /challenge/run to get our flag.
We first cd into ```/tmp``` and then create the new files.
```
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ ls
bin  college  hsperfdata_root  pwn  tmp.XvrUsDZh8M
hacker@commands~touching-files:/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{01aEK_EVa_Dau7tdfQVhBL5PIad.dBzM4QDLygDO0czW}
```
## removing files 
In Linux, you remove files with the rm command.
The syntax for rm command: ```hacker@dojo:~$ rm filename ```
In this challenge we have to remove a delete_me file in your home directory and, then run /challenge/check.
```
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{c0VSND-5Tn730iC1iXj1j8ha4XA.dZTOwUDLygDO0czW}
```
## hidden files 
ls doesn't list all the files by default. Linux has a convention where files that start with a . don't show up by default in ls. <br>
To view them with ls, you need to invoke ls with the -a flag.
```hacker@dojo:~$ ls -a```
In this challenge we have to find the flag, hidden as a dot-prepended file in /.
```
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls -a
.           .flag-25382926915388  challenge  home   lib64   mnt  proc  sbin  tmp
..          bin                   dev        lib    libx32  nix  root  srv   usr
.dockerenv  boot                  etc        lib32  media   opt  run   sys   var
hacker@commands~hidden-files:/$ cat .flag-25382926915388
pwn.college{0q4OPGKmQuGE10alaZFpIggGcZ0.dBTN4QDLygDO0czW}
```
## An epic filesystem quest
In this challenge we make use of our knowledge of cd,ls and cat.
In this challenge the flag is hidden. The goal is to find the flag.
We are provided with the following clues.
Your first clue is in /. Head on over there.<br>
Look around with ls. There'll be a file named HINT or CLUE or something along those lines!<br>
cat that file to read the clue!<br>
Depending on what the clue says, head on over to the next directory (or don't!).<br>
Follow the clues to the flag!<br>
```
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
SPOILER  challenge  flag  lib32   media  opt   run   sys  var
bin      dev        home  lib64   mnt    proc  sbin  tmp
boot     etc        lib   libx32  nix    root  srv   usr
hacker@commands~an-epic-filesystem-quest:/$ cat SPOILER
Great sleuthing!
The next clue is in: /usr/share/racket/pkgs/draw-lib/racket/draw/unsafe/compiled

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
```
After we cd into the given direcotry we use the ``` ls -a``` command because we know that the filename starts with .
```
hacker@commands~an-epic-filesystem-quest:/$ cd /usr/share/racket/pkgs/draw-lib/racket/draw/unsafe/compiled
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/draw-lib/racket/draw/unsafe/compiled$ ls
brush_rkt.dep  cairo-lib_rkt.dep  glib_rkt.dep  pango_rkt.dep
brush_rkt.zo   cairo-lib_rkt.zo   glib_rkt.zo   pango_rkt.zo
bstr_rkt.dep   cairo_rkt.dep      jpeg_rkt.dep  png_rkt.dep
bstr_rkt.zo    cairo_rkt.zo       jpeg_rkt.zo   png_rkt.zo
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/draw-lib/racket/draw/unsafe/compiled$ ls -a
.              brush_rkt.zo       cairo-lib_rkt.zo  glib_rkt.zo    pango_rkt.zo
..             bstr_rkt.dep       cairo_rkt.dep     jpeg_rkt.dep   png_rkt.dep
.POINTER       bstr_rkt.zo        cairo_rkt.zo      jpeg_rkt.zo    png_rkt.zo
brush_rkt.dep  cairo-lib_rkt.dep  glib_rkt.dep      pango_rkt.dep
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/draw-lib/racket/draw/unsafe/compiled$ cat .POINTER
Congratulations, you found the clue!
The next clue is in: /usr/share/icons/Humanity/devices/24
```
The first case is what happens when you run ```ls``` and not ```ls -a``
```
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/draw-lib/racket/draw/unsafe/compiled$ cd /usr/share/icons/Humanity/devices/24
hacker@commands~an-epic-filesystem-quest:/usr/share/icons/Humanity/devices/24$ ls
3floppy_unmount.svg                 gtk-harddisk.svg
MESSAGE                             gtkpod.svg
audio-input-microphone.svg          harddrive.svg
battery.svg                         hdd_unmount.svg
block-device.svg                    input-keyboard.svg
camera-photo.svg                    input-mouse.svg
camera-web.svg                      ipod_mount.svg
camera_unmount.svg                  keyboard.svg
cdrom_unmount.svg                   kjobviewer.svg
cdwriter_unmount.svg                kxkb.svg
chardevice.svg                      media-cdr.svg
computer.svg                        media-cdrom-audio.svg
display.svg                         media-cdrom.svg
drive-cdrom.svg                     media-cdrw.svg
drive-harddisk-ieee1394.svg         media-dvd.svg
drive-harddisk-scsi.svg             media-dvdrw.svg
drive-harddisk-usb.svg              media-flash-cf.svg
drive-harddisk.svg                  media-flash-ms.svg
drive-optical.svg                   media-flash.svg
drive-removable-media-ieee1394.svg  media-floppy.svg
drive-removable-media-usb.svg       media-jaz.svg
drive-removable-media.svg           media-memory-sd.svg
dvd_unmount.svg                     media-memory-sm.svg
gnome-cd.svg                        media-optical-audio.svg
gnome-computer.svg                  media-optical-cd-r.svg
gnome-dev-battery.svg               media-optical-cd-rw.svg
gnome-dev-cdrom-audio.svg           media-optical-cd.svg
gnome-dev-cdrom.svg                 media-optical-cdr.svg
gnome-dev-computer.svg              media-optical-dvd-r-plus.svg
gnome-dev-disc-audio.svg            media-optical-dvd-r.svg
gnome-dev-disc-cdr.svg              media-optical-dvd-ram.svg
gnome-dev-disc-cdrom.svg            media-optical-dvd-rom.svg
gnome-dev-disc-cdrw.svg             media-optical-dvd-rw.svg
gnome-dev-disc-dvdr-plus.svg        media-optical-dvd.svg
gnome-dev-disc-dvdr.svg             media-optical.svg
gnome-dev-disc-dvdram.svg           monitor.svg
gnome-dev-disc-dvdrom.svg           mouse.svg
gnome-dev-disc-dvdrw.svg            multimedia-player-apple-ipod-touch.svg
gnome-dev-dvd-alt.svg               multimedia-player-apple-ipod.svg
gnome-dev-dvd.svg                   multimedia-player-ipod-touch.svg
gnome-dev-ethernet.svg              multimedia-player-ipod.svg
gnome-dev-flashdisk.svg             multimedia-player.svg
gnome-dev-flashkey.svg              music-player.svg
gnome-dev-floppy.svg                network-wired.svg
gnome-dev-harddisk-1394.svg         network-wireless.svg
gnome-dev-harddisk-usb.svg          network-workgroup.svg
gnome-dev-harddisk.svg              network_fs.svg
gnome-dev-ipod.svg                  nfs.svg
gnome-dev-jazdisk.svg               nm-device-wired.svg
gnome-dev-keyboard.svg              pda.svg
gnome-dev-media-cf.svg              phone-motorola-droid.svg
gnome-dev-media-memory.svg          phone.svg
gnome-dev-media-ms.svg              printer-remote.svg
gnome-dev-media-sdmmc.svg           printer.svg
gnome-dev-media-sm.svg              printer1.svg
gnome-dev-mouse-ball.svg            printmgr.svg
gnome-dev-mouse-optical.svg         samba.svg
gnome-dev-network.svg               stock_cell-phone.svg
gnome-dev-printer.svg               stock_mic.svg
gnome-dev-removable-1394.svg        stock_printers.svg
gnome-dev-removable-usb.svg         system-floppy.svg
gnome-dev-removable.svg             system.svg
gnome-dev-trash-empty.svg           usbpendrive_unmount.svg
gnome-dev-trash-full.svg            video-display.svg
gnome-dev-unknown-1394.svg          xfce-printer.svg
gnome-dev-unknown-usb.svg           xfce4-display.svg
gnome-dev-wavelan.svg               xfce4-keyboard.svg
gnome-fs-client.svg                 xfce4-mouse.svg
gnome-phone-manager.svg             yast_HD.svg
gnome-stock-mic.svg                 yast_idetude.svg
gtk-cdrom.svg                       yast_mouse.svg
gtk-floppy.svg                      yast_printer.svg
hacker@commands~an-epic-filesystem-quest:/usr/share/icons/Humanity/devices/24$ cat MESSAGE
Great sleuthing!
The next clue is in: /opt/linux/linux-5.4/arch/sh/include/uapi/asm

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
```
We ```cd``` into the required directory and run ```ls```.
```
hacker@commands~an-epic-filesystem-quest:/usr/share/icons/Humanity/devices/24$ cd /opt/linux/linux-5.4/arch/sh/include/uapi/asm
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/sh/include/uapi/asm$ ls
INFO         cpu-features.h    posix_types_64.h  sigcontext.h  types.h
Kbuild       hw_breakpoint.h   ptrace.h          signal.h      unistd.h
auxvec.h     ioctls.h          ptrace_32.h       sockios.h     unistd_64.h
byteorder.h  posix_types.h     ptrace_64.h       stat.h
cachectl.h   posix_types_32.h  setup.h           swab.h
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/sh/include/uapi/asm$ cat INFO
Great sleuthing!
The next clue is in: /usr/lib/python3/dist-packages/sympy/parsing/autolev/__pycache__
```
After ```cd```ing to the directory and running ```ls```
```
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/sh/include/uapi/asm$ cd /usr/lib/python3/dist-packages/sympy/parsing/autolev/__pycache__
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/sympy/parsing/autolev/__pycache__$ ls
BRIEF                    _listener_autolev_antlr.cpython-38.pyc
__init__.cpython-38.pyc  _parse_autolev_antlr.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/sympy/parsing/autolev/__pycache__$ cat BRIEF
Tubular find!
The next clue is in: /usr/share/racket/pkgs/htdp-lib/xml

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
```
We know that we have to use ```ls -a``` to list the files in the upcoming directory.
```
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/sympy/parsing/autolev/__pycache__$ cd /usr/share/racket/pkgs/htdp-lib/xml
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/htdp-lib/xml$ ls -a
.   .DISPATCH  info.rkt              text-box-tool.rkt   xml-snipclass.rkt
..  compiled   scheme-snipclass.rkt  text-snipclass.rkt  xml.png
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/htdp-lib/xml$
```
We can now use ```cat``` to read the ```.DISPATCH``` file
```
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/htdp-lib/xml$ cat .DISPATCH
Lucky listing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/Crypto/SelfTest/Util/__pycache__
```
```
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/htdp-lib/xml$ cd  /usr/local/lib/python3.8/dist-packages/Crypto/SelfTest/Util/__pycache__
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/Crypto/SelfTest/Util/__pycache__$ ls
MEMO                         test_asn1.cpython-38.pyc
__init__.cpython-38.pyc      test_number.cpython-38.pyc
test_Counter.cpython-38.pyc  test_rfc1751.cpython-38.pyc
test_Padding.cpython-38.pyc  test_strxor.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/Crypto/SelfTest/Util/__pycache__$ cat MEMO
Congratulations, you found the clue!
The next clue is in: /usr/share/git-core/templates
```
```
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/Crypto/SelfTest/Util/__pycache__$ cd /usr/share/git-core/templates
hacker@commands~an-epic-filesystem-quest:/usr/share/git-core/templates$ ls
NOTE  branches  description  hooks  info
hacker@commands~an-epic-filesystem-quest:/usr/share/git-core/templates$ cat NOTE
Lucky listing!
The next clue is in: /opt/aflplusplus/testcases/archives/exotic/lrzip

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
```
Because the next clue is trapped we cant ```cd``` into the file.
Hence we use ```ls``` and the absolute path.
```
hacker@commands~an-epic-filesystem-quest:/usr/share/git-core/templates$ ls /opt/aflplusplus/testcases/archives/exotic/lrzip
WHISPER-TRAPPED  small_archive.lrz
```
```
hacker@commands~an-epic-filesystem-quest:/usr/share/git-core/templates$ cat /opt/aflplusplus/testcases/archives/exotic/lrzip/WHISPER-TRAPPED
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{QNQwOK9DWeO0KfBUq91VyAchdyN.dljM4QDLygDO0czW}
```
## making directories 
In this challenge we learn to use the ```mkdir``` command which is used to make new directories.
In the challenge we must create a /tmp/pwn directory and make a college file in it. Then run /challenge/run, which will check our solution and give use the flag.
```
hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ cd /tmp/pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ cd
hacker@commands~making-directories:~$ /challenge/run
Success! Here is your flag:
pwn.college{8dYzbGj1fABMmLlw6CEFmAw8YSM.dFzM4QDLygDO0czW}
```
## Finding files 
In this challenge the goal is to find a file names ```flag```, and as multiples files exist we read all the files using ```cat``` until we find the flag.
```
hacker@commands~finding-files:~$ find / -name flag
find: ‘/root’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/7/task/7/fd’: Permission denied
find: ‘/proc/7/task/7/fdinfo’: Permission denied
find: ‘/proc/7/task/7/ns’: Permission denied
find: ‘/proc/7/fd’: Permission denied
find: ‘/proc/7/map_files’: Permission denied
find: ‘/proc/7/fdinfo’: Permission denied
find: ‘/proc/7/ns’: Permission denied
find: ‘/var/log/private’: Permission denied
find: ‘/var/log/apache2’: Permission denied
find: ‘/var/log/mysql’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/php/sessions’: Permission denied
find: ‘/var/lib/mysql-files’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/mysql-keyring’: Permission denied
find: ‘/var/lib/mysql’: Permission denied
find: ‘/tmp/tmp.XvrUsDZh8M’: Permission denied
find: ‘/run/mysqld’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/local/share/radare2/5.9.5/flag
/usr/lib/ruby/2.7.0/bundler/templates/newgem/spec/flag
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
/opt/radare2/libr/flag
/nix/store/pmvk2bk4p550w182rjfm529kfqddnvh3-python3.11-pwntools-4.12.0/lib/python3.11/site-packages/pwnlib/flag
/nix/store/1yagn5s8sf7kcs2hkccgf8d0wxlrv5sz-radare2-5.9.0/share/radare2/5.9.0/flag
hacker@commands~finding-files:~$ cat /usr/local/lib/python3.8/dist-packages/pwnlib/flag
cat: /usr/local/lib/python3.8/dist-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ ls /usr/local/lib/python3.8/dist-packages/pwnlib/flag
__init__.py  __pycache__  flag.py
hacker@commands~finding-files:~$ cat /usr/local/share/radare2/5.9.5/flag
cat: /usr/local/share/radare2/5.9.5/flag: Is a directory
hacker@commands~finding-files:~$ ls /usr/local/share/radare2/5.9.5/flag
tags.r2
hacker@commands~finding-files:~$ cat /usr/lib/ruby/2.7.0/bundler/templates/newgem/spec/flag
hacker@commands~finding-files:~$ cat /usr/lib/ruby/2.7.0/bundler/templates/newgem/spec/flag
pwn.college{wpwNNt06poEWlhDhAwBPtFlwuGC.dJzM4QDLygDO0czW}
```
## Linking files
Symbolic links are created with the ```ln``` command with the ```-s``` argument. In this level the flag is, as always, in /flag, but /challenge/catflag will instead read out /home/hacker/not-the-flag. Using the symlink we trick it into giving us the flag.
```
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
cat: /home/hacker/not-the-flag: No such file or directory
hacker@commands~linking-files:~$ ln -s /flag ~/not-the-flag
hacker@commands~linking-files:~$ challenge/catflag
ssh-entrypoint: challenge/catflag: No such file or directory
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
pwn.college{E-TQY1Y4x0wg1tqGYx6paZYTaxD.dlTM1UDLygDO0czW}
```
And that's the end of module three.



