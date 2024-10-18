# Untangling Users
## Becoming root with su 
In this challenge we learn how to use the ```su``` switch user command.

```
hacker@users~becoming-root-with-su:~$ su
Password: 
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{wqISaC-jjYddmnLy-sw9QQXBVhz.dVTN0UDLygDO0czW}
```
## Other users with su 
With no arguments, su will start a root shell.
However, we can also give a username as an argument to switch to that user instead of root.
In this level, we must switch to the zardus user and then run /challenge/run.
```
hacker@users~other-users-with-su:~$ su zardus 
Password: 
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{wRlegVoWAznOCuU5ydoaYRofVYv.dZTN0UDLygDO0czW}
```
## Cracking passwords 
When you enter a password for su, it compares it against the stored password for that user.
These passwords used to be stored in /etc/passwd, but because /etc/passwd is a globally-readable file,
these were moved to /etc/shadow.
Separated by :s, the first field of each line is the username and the second is the password. A value of * or ! functionally means that password login for the account is disabled, a blank field means that there is no password.
what if we don't know the password? if we have the hashed value of the password we can figure it out.
```
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
aardvark         (zardus)
1g 0:00:00:20 100% 2/3 0.04863g/s 283.2p/s 283.2c/s 283.2C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@users~cracking-passwords:~$ su zardus 
Password: 
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{4ZR80Fdd2aDrAwTDO4zQ_5DT8sc.ddTN0UDLygDO0czW}
```

## Using sudo
Unlike su, which defaults to launching a shell as a specified user, sudo defaults to running a command as root.
```
hacker@users~using-sudo:~$ sudo cat /flag
pwn.college{4DCi-JtV-reKndKWQP_xDmzMxav.dhTN0UDLygDO0czW}
hacker@users~using-sudo:~$ cat /flag
cat: /flag: Permission denied
```
trial 2 is what happens if we dont use ```sudo```





