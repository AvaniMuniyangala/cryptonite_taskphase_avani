# Perceiving Permissions
## Changing File ownership 
we can check out a permissions of a file or directory using ```ls -l```.
Every file in Linux is owned by a user on the system.
The two most important user accounts are: <br>
1.Your user account.<br>
2.root. This is the administrative account.<br>
We can change the ownership of files! This is done via the chown (change owner) command.
In this level we practice changing the owner of the /flag file to the hacker user.
```
ls -hacker@permissions~changing-file-ownership:~$ ls -l
total 24
-rw-r--r-- 1 hacker hacker    4 Oct  9 12:48 COLLEGE
drwxr-xr-x 2 hacker hacker 4096 Oct  1 15:03 Desktop
-rw-r--r-- 1 hacker hacker    0 Oct 12 12:20 PWN
-rw-r--r-- 1 root   hacker   58 Oct  8 18:33 a
-rw-r--r-- 1 hacker hacker    0 Oct  9 06:48 college
-rw-r--r-- 1 hacker hacker  829 Oct  9 16:49 instructions
-rw-r--r-- 1 hacker hacker   77 Oct  9 17:20 myflag
lrwxrwxrwx 1 hacker hacker    5 Oct  9 10:08 not-the-flag -> /flag
-rw-r--r-- 1 hacker hacker  435 Oct  9 16:42 the-flag
hacker@permissions~changing-file-ownership:~$ chown hacker not-the-flag
hacker@permissions~changing-file-ownership:~$ cat no-the-flag
cat: no-the-flag: No such file or directory
hacker@permissions~changing-file-ownership:~$ cat not-the-flag
pwn.college{IC3sEoFNSGdg0AyO017qkJ83Ngg.dFTM2QDLygDO0czW}
```
## Groups and Files 
Files have both an owning user and group. A group can have multiple users in it, and a user can be a member of multiple groups.

In this level the flag is readable only by the group that owns it. Here the group is root.
Upon changing the ownership of the flag file we recieve the flag.
```
hacker@permissions~groups-and-files:~$ ls -ll
total 24
-rw-r--r-- 1 hacker hacker    4 Oct  9 12:48 COLLEGE
drwxr-xr-x 2 hacker hacker 4096 Oct  1 15:03 Desktop
-rw-r--r-- 1 hacker hacker    0 Oct 12 12:20 PWN
-rw-r--r-- 1 root   hacker   58 Oct  8 18:33 a
-rw-r--r-- 1 hacker hacker    0 Oct  9 06:48 college
-rw-r--r-- 1 hacker hacker  829 Oct  9 16:49 instructions
-rw-r--r-- 1 hacker hacker   77 Oct  9 17:20 myflag
lrwxrwxrwx 1 hacker hacker    5 Oct  9 10:08 not-the-flag -> /flag
-rw-r--r-- 1 hacker hacker  435 Oct  9 16:42 the-flag
hacker@permissions~groups-and-files:~$ chgrp hacker /flag
hacker@permissions~groups-and-files:~$ cat /flag
pwn.college{QEHJa-ZM22_VZi5yOISGv0z_dy8.dFzNyUDLygDO0czW}
```
## Fun with group names 
In this challenge we have to figure out the name using ```id```.
```
hacker@permissions~fun-with-groups-names:~$ ls -l
total 24
-rw-r--r-- 1 hacker grp16497    4 Oct  9 12:48 COLLEGE
drwxr-xr-x 2 hacker grp16497 4096 Oct  1 15:03 Desktop
-rw-r--r-- 1 hacker grp16497    0 Oct 12 12:20 PWN
-rw-r--r-- 1 root   grp16497   58 Oct  8 18:33 a
-rw-r--r-- 1 hacker grp16497    0 Oct  9 06:48 college
-rw-r--r-- 1 hacker grp16497  829 Oct  9 16:49 instructions
-rw-r--r-- 1 hacker grp16497   77 Oct  9 17:20 myflag
lrwxrwxrwx 1 hacker grp16497    5 Oct  9 10:08 not-the-flag -> /flag
-rw-r--r-- 1 hacker grp16497  435 Oct  9 16:42 the-flag
hacker@permissions~fun-with-groups-names:~$ id hacker 
uid=1000(hacker) gid=1000(grp16497) groups=1000(grp16497)
hacker@permissions~fun-with-groups-names:~$ chgrp grp16497 /flag
hacker@permissions~fun-with-groups-names:~$ cat /flag
pwn.college{ATVKUroMQn3GywqT32Yq8K2Tp7p.dJzNyUDLygDO0czW}
```
## Changing permissions 
The first character there is the file type.The next nine characters are the actual access permissions of the file or directory, split into 3 characters denoting permissions for the owning user
,3 characters denoting the permissions for the owning group, and 3 characters denoting the permissions that all other access.<br>
r - can read the file or list the directory<br>
w - can modify the files or create/delete files in the directory<br>
x - can execute the file as a program or can enter the directory<br>
- - nothing <br>
The basic usage for chmod is:<br>

```chmod [options] MODE FILE```
In this challenge we need to change the permissions of the flag file to read it.
```
hacker@permissions~changing-permissions:~$ ls -l
total 24
-rw-r--r-- 1 hacker hacker    4 Oct  9 12:48 COLLEGE
drwxr-xr-x 2 hacker hacker 4096 Oct  1 15:03 Desktop
-rw-r--r-- 1 hacker hacker    0 Oct 12 12:20 PWN
-rw-r--r-- 1 root   hacker   58 Oct  8 18:33 a
-rw-r--r-- 1 hacker hacker    0 Oct  9 06:48 college
-rw-r--r-- 1 hacker hacker  829 Oct  9 16:49 instructions
-rw-r--r-- 1 hacker hacker   77 Oct  9 17:20 myflag
lrwxrwxrwx 1 hacker hacker    5 Oct  9 10:08 not-the-flag -> /flag
-rw-r--r-- 1 hacker hacker  435 Oct  9 16:42 the-flag
hacker@permissions~changing-permissions:~$ chmod o+r /flag
hacker@permissions~changing-permissions:~$ cat /flag
pwn.college{4R4wONAvnxp_e3pr_9-pv5koGqn.dNzNyUDLygDO0czW}
```
We first ls -l to find the /flag permissions.
Then we use ```chmod``` so we can read the program using ```cat```.
## Executable files 
In this challenge, the /challenge/run program will give you the flag, but we must first make it executable.
```
hacker@permissions~executable-files:~$ ls -l /challenge/run
-r--r--r-- 1 hacker hacker 32 Jul  4 06:37 /challenge/run
hacker@permissions~executable-files:~$ chmod ugo+x /challenge/run
hacker@permissions~executable-files:~$ /challenge/run 
Successful execution! Here is your flag:
pwn.college{gLYUZVRj4JLhKrrwi_4ZcfygDoP.dJTM2QDLygDO0czW}
```
```ugo+x``` grants everyone teh access to execute the program .
## Permission tweaking practice
practice of ```chmod```
We /challenge/run first as asked.

```
hacker@permissions~permission-tweaking-practice:~$ /challenge/run 
Round 0 (of 8)!

Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rw-------
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
```
hacker@permissions~permission-tweaking-practice:~$ chmod go-r /challenge/pwn
You set the correct permissions!
Round 1 (of 8)!

Current permissions of "/challenge/pwn": rw-------
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r--------
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
```
hacker@permissions~permission-tweaking-practice:~$ chmod u-w /challenge/pwn
You set the correct permissions!
Round 2 (of 8)!

Current permissions of "/challenge/pwn": r--------
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r---w--w-
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod go+w /challenge/pwn
You set the correct permissions!
```
```
Round 3 (of 8)!

Current permissions of "/challenge/pwn": r---w--w-
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rw--w--w-
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
```
```
hacker@permissions~permission-tweaking-practice:~$ chmod u+w /challenge/pwn
You set the correct permissions!
Round 4 (of 8)!

Current permissions of "/challenge/pwn": rw--w--w-
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -w--w--w-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
```
```
hacker@permissions~permission-tweaking-practice:~$ chmod u-r /challenge/pwn
You set the correct permissions!
Round 5 (of 8)!

Current permissions of "/challenge/pwn": -w--w--w-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
```
hacker@permissions~permission-tweaking-practice:~$ chmod ugo-w /challenge/pwn
You set the correct permissions!
Round 6 (of 8)!

Current permissions of "/challenge/pwn": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -wx----wx
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
* the world does have execute permissions
```
```
hacker@permissions~permission-tweaking-practice:~$ chmod uo+wx /challenge/pwn
You set the correct permissions!
Round 7 (of 8)!

Current permissions of "/challenge/pwn": -wx----wx
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": -wx---rwx
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions
```
```
hacker@permissions~permission-tweaking-practice:~$ chmod o+r /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod ugo+r /flag
hacker@permissions~permission-tweaking-practice:~$ cat /flag
pwn.college{IJ80RqVZqitCCOos5Xc5TPAyeE5.dBTM2QDLygDO0czW}
```
Multiple typos resulted in me doing this multiple times.

## Permissions setting practice
chmod can also overwrite permissions.
1.u=rw sets read and write permissions for the user, and wipes the execute permission<br>
2.o=x sets only executable permissions for the world, wiping read and write<br>
3.a=rwx sets read, write, and executable permissions for the user, group, and world<br>
I first /challenge/run as told.
```
hacker@permissions~permissions-setting-practice:~$ /challenge/run
Round 0 (of 8)!

Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwx-w-r-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permission
```
User needed the read write and execute permissions.Group only write and world only read and execute.
```
hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=w,o=rx /challenge/pwn
You set the correct permissions!
Round 1 (of 8)!

Current permissions of "/challenge/pwn": rwx-w-r-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rw--wxr--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
```
hacker@permissions~permissions-setting-practice:~$ chmod u=rw,g=wx,o=r /challenge/pwn
You set the correct permissions!
Round 2 (of 8)!

Current permissions of "/challenge/pwn": rw--wxr--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxrwx-w-
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
```
```
hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=rwx,o=w /challenge/pwn
You set the correct permissions!
Round 3 (of 8)!

Current permissions of "/challenge/pwn": rwxrwx-w-
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": --xr-x---
- the user doesn't have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
```
hacker@permissions~permissions-setting-practice:~$ chmod u=x,g=rx,o=- /challenge/pwn
You set the correct permissions!
Round 4 (of 8)!

Current permissions of "/challenge/pwn": --xr-x---
- the user doesn't have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwx--xrw-
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
```
```
hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=x,o=rw /challenge/pwn
You set the correct permissions!
Round 5 (of 8)!

Current permissions of "/challenge/pwn": rwx--xrw-
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -w-----wx
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
* the world does have execute permissions
```
```
hacker@permissions~permissions-setting-practice:~$ chmod u=w,g=-,o=wx /challenge/pwn
You set the correct permissions!
Round 6 (of 8)!

Current permissions of "/challenge/pwn": -w-----wx
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": -w--wxrw-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

```
```
hacker@permissions~permissions-setting-practice:~$ chmod u=w,g=wx,o=rw /challenge/pwn
You set the correct permissions!
Round 7 (of 8)!

Current permissions of "/challenge/pwn": -w--wxrw-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": ---rwx--x
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
```
```
hacker@permissions~permissions-setting-practice:~$ chmod u=-,g=rwx,o=x /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=rwx,o=rwx /flag
hacker@permissions~permissions-setting-practice:~$ cat /flag
pwn.college{Mov9cSpEEn-89NkLBnWtuAxtLoU.dNTM5QDLygDO0czW}
```




## The SUID bit 
The "Set User ID" (SUID) permissions bit allows the user to run a program as the owner of that program's file.
```
hacker@permissions~the-suid-bit:~$ ls -l /challenge/getroot
-rwxr-xr-x 1 root root 155 Jul 12 10:30 /challenge/getroot
hacker@permissions~the-suid-bit:~$ chmod u+s /challenge/getroot
hacker@permissions~the-suid-bit:~$ /challenge/getroot
SUCCESS! You have set the suid bit on this program, and it is running as root! 
Here is your shell...
root@permissions~the-suid-bit:~# cat /flag
pwn.college{gMoSx1j7-wIcnH4wgq3YTIr7UMD.dNTM2QDLygDO0czW}
```
Module 9



