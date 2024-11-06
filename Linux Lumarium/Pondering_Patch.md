# Pondering Paths

## The Root
So in this challenge we are told that the filesystem starts at /.
A program can by invoked by providing its path on the command line. The style of path, one that starts with the root directory (/), is referred to as an "absolute path".
In this challenge we are asked to invoke the pwn program using its absolute path.
```
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{AAu2N-ZCeY39wFz4-Q5B7BmAzbP.dhzN5QDLygDO0czW}
```
## Program and absolute paths 
In this challenge we have to access a slightly more complicated absolute path and we are awarded the flag.
```
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{sujRPDeSSa74qbqG17vR7WKzrgl.dVDN1QDLygDO0czW}
```
## Position thy self 
We navigate around directories by using the cd (change directory).
When we use the cd command our cwd (current working directory) is changed.
In this challenge we are asked to cd into a directory that will be revealed to us once we ```/challenge/run```
Upon running ```/challenge/run```
```
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /usr/bin directory.
Please use the `cd` utility to change directory appropriately
```
We then cd into the required directory and ```/challenge/run``` again.
```
hacker@paths~position-thy-self:~$  cd /usr/bin 
hacker@paths~position-thy-self:/usr/bin$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{Q-h65WgkSkdxx26k5pK8Nk3esll.dZDN1QDLygDO0czW}
```
## Position elsewhere
NOTE: The symbol ~ shows the current your shell is located in. <br>
In this challenge we first run ```/challenge/run``` and it directs us to the directory we need to cd into.
```
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /home directory.
Please use the `cd` utility to change directory appropriately.
```
We then change directories to home directory using ```cd``` command.
```
hacker@paths~position-elsewhere:~$ cd /home
```
We then ```/challenge/run``` to obtain the flag
```
hacker@paths~position-elsewhere:/home$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{EFSpD4f3ZkLupjm2TPMSw9qgiw1.ddDN1QDLygDO0czW}
```
## Position yet elsewhere 
This challenge is similar to the previous in terms of logic.
```
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /sys directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-yet-elsewhere:~$ cd /sys
hacker@paths~position-yet-elsewhere:/sys$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{wU5DQ1qBH4vhSG6DPapdAx7Fe7f.dhDN1QDLygDO0czW}
```
## implicit relative paths , from /
So far we have been using absolute paths (paths that start at root). We will now use relative paths.
A relative path is interpreted relative to your current working directory (cwd).
Your cwd is the directory that your prompt is currently located at.
In this challenge we have to run ```/challenge/run``` using a relative path.
We first ```cd``` into the / directory 
Then our relative path becomes ```challenge/run```
```
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{8fjWn1SnAjdHwuIT8jDosSdOf9c.dlDN1QDLygDO0czW}
```
## explicit relative paths, from /
The following absolute paths are all identical to each other: <br>
1) /challenge <br>
2) /challenge/. <br>
3) /challenge/./././././././././ <br>
4) /./././challenge/././ <br>
The following relative paths are also all identical to each other: <br>
1) challenge <br>
2) ./challenge <br>
3) ./././challenge <br>
4) challenge/. <br>
The challenge wants us to use . in our relative paths.
```
hacker@paths~explicit-relative-paths-from-:/challenge$ cd /
hacker@paths~explicit-relative-paths-from-:/$ ././challenge/run
Correct!!!
././challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{EqADWEw0Khw7eezMasecqP00dhE.dBTN1QDLygDO0czW}
```
## implicit relative path 
In linux when you invoke ```/challenge/run``` the command is not executed. This is part of a safety measure. In order to tell Linux that you explicitly want to execute a program in the current directory, we use .
```
hacker@paths~implicit-relative-path:~$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{8_Ku1uqrYWMFuJXerqDctYGhUqk.dFTN1QDLygDO0czW}
```
## home sweet home 
In this challenge, /challenge/run will write a copy of the flag to any file you specify as an argument.
```
hacker@paths~home-sweet-home:~$ /challenge/run ~/a
Writing the file to /home/hacker/a!
... and reading it back to you:
pwn.college{k0nCn7V7JARetmoPpxfBLOwET5t.dNzM4QDLygDO0czW}
```
Here I chose a as my argument simply because it fit all the constraints given in the challenge description.

Thus ends the second module.





