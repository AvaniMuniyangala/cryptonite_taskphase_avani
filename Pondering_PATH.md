# Pondering PATH
## The PATH variable
There is a special shell variable, called PATH, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands.
Without a PATH, bash cannot find the ls command.
In this challenge we prevent the program from deleting the flag by removing the remove command.

```
hacker@path~the-path-variable:~$ ls
COLLEGE  a         college       not-the-flag  x.sh
Desktop  a.sh      instructions  the-flag
PWN      avani.sh  myflag        x
hacker@path~the-path-variable:~$ PATH=""
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{MTnzC8yorHR_m1ZIDCsT0REMEdz.dZzNwUDLygDO0czW}
```
## Setting PATH
In this challenge we learn how to add a new directory of programs to our command repertoire.
```
hacker@path~setting-path:~$ PATH=/challenge/more_commands/
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{AtWGduYHHlvoSiBtrlsITiVukJu.dVzNyUDLygDO0czW}
```
## Adding commands 
Multiple tries later
```
hacker@path~adding-commands:~$ touch win
hacker@path~adding-commands:~$ nano win
```
```
chmod a+x win; cat /flag
```

```
hacker@path~adding-commands:~$ echo $PATH
/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~adding-commands:~$ PATH=$PATH:/home/hacker
hacker@path~adding-commands:~$ /challenge/run 
Invoking 'win'....
pwn.college{kfCNJupDwE-mJYLU-2lLHRhKetk.dZzNyUDLygDO0czW}
```
## Hijacking commands 
```
hacker@path~hijacking-commands:~$ touch rm
hacker@path~hijacking-commands:~$ nano rm
hacker@path~hijacking-commands:~$ echo $PATH
/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~hijacking-commands:~$ PATH=/home/hacker:/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
Found 'rm' command at /home/hacker/rm. Executing!
hacker@path~hijacking-commands:~$ nano rm
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
Found 'rm' command at /home/hacker/rm. Executing!
rm FOUND!!!!
```
no flag given unfortunately 
added a cat /flag to rm
```
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
Found 'rm' command at /home/hacker/rm. Executing!
rm FOUND!!!!
pwn.college{khm4RpVCGM1pCeVU8LCMYXUuAFG.ddzNyUDLygDO0czW}
```
flag given fortunately



