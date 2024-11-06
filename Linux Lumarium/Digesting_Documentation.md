# Digesting Documentation
## Learning from documentation 
The program for this challenge is /challenge/challenge, and we need to invoke it properly in order for it to give us the flag.
In the challenge description it is specified that the argument we need to use in order to reciece the glad is ```--giveflag```
```
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{ECSoDHZk0Z1qv6kBL8KFvEybzro.dRjM5QDLygDO0czW}
```
## Learning complex usage 
```find``` has a ```-name``` argument, and the ```-name``` argument itself takes an argument specifying the name to search for
```
hacker@man~learning-complex-usage:~$ ls 
Desktop  a  college  not-the-flag
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile not-the-flag
Correct argument! Here is the not-the-flag file:
pwn.college{4_oJFd_ywX50NNyvKyeM12hzHyh.dVjM5QDLygDO0czW}
```
In this challenge we use not-the-flag as the argument to ```-printfile```
## Reading Manuals 
This level introduces the man command. man is short for manual, and will display the manual of the command you pass as an argument.
When you're done reading the manpage, you can hit q to quit.
The challenge in this level has a secret option that, when you use it, will cause the challenge to print the flag. 
We are asked to find this option through the man page for challenge.
```
hacker@man~reading-manuals:~$ man challenge

CHALLENGE(1)               Challenge Commands              CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --kacnar NUM
              print the flag if NUM is 482

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The   repository   for  this  dojo:  <https://github.com/pwncol‐
       lege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                     May 2024                   CHALLENGE(1)
```
We learn that the secret option is 
```
--kacnar NUM
print the flag if NUM is 482
```
So accordingly, 
```
hacker@man~reading-manuals:~$ /challenge/challenge --kacnar 482
Correct usage! Your flag: pwn.college{Ik4acn8aZH230r9dRJ7tBSLXvGQ.dRTM4QDLygDO0czW}
```
## Searching manuals 
In this challenge we are taught how to search though manuals using ```n``` ```N``` ```/``` ```?```.
I noticed that all the arugments that would not give us the flag had the description ```A neat argument, but not the right one```.
Using that phrase and ```?``` I searched through the manual.
It simplied my process of searching as all i had to do was find the non highlighted text
After a good while of searching.
``` --swo  This argument will give you the flag!```
Then I just 
```
hacker@man~searching-manuals:~$ man challenge
hacker@man~searching-manuals:~$ /challenge/challenge --swo
Initializing...
Correct usage! Your flag: pwn.college{cFQOPqPoDO7r_omJ20rUARR7Cia.dVTM4QDLygDO0czW}
```
## Searhing for manuals
Using the hints 
HINT 1: man man teaches you advanced usage of the man command itself, and you must use this knowledge to figure out how to search for the hidden manpage that will tell you how to use /challenge/challenge<br>

HINT 2: though the man page is randomly named, you still actually use /challenge/challenge to get the flag!<br>
We use ```man man ``` to find the manual for ```man```. And then we search through the manual to find the ```challenge``` manual.
```
hacker@man~searching-for-manuals:~$ man man 
MAN(1)                     Manual pager utils                    MAN(1)

NAME
       man - an interface to the system reference manuals

SYNOPSIS
       man [man options] [[section] page ...] ...
       man -k [apropos options] regexp ...
       man -K [man options] [section] term ...
       man -f [whatis options] page ...
       man -l [man options] file ...
       man -w|-W [man options] page ...

DESCRIPTION
       man  is  the system's manual pager.  Each page argument given to
       man is normally the name of a program, utility or function.  The
       manual  page  associated  with  each  of these arguments is then
       found and displayed.  A section, if provided, will direct man to
       look  only in that section of the manual.  The default action is
       to search in all of the available sections following  a  pre-de‐
       fined  order  (see  DEFAULTS),  and  to show only the first page
       found, even if page exists in several sections.

       The table below shows the section numbers of the manual followed
       by the types of pages they contain.

       1   Executable programs or shell commands
       2   System calls (functions provided by the kernel)
       3   Library calls (functions within program libraries)
       4   Special files (usually found in /dev)
       5   File formats and conventions, e.g. /etc/passwd
       6   Games
       7   Miscellaneous  (including  macro  packages and conventions),
           e.g. man(7), groff(7)
       8   System administration commands (usually only for root)
       9   Kernel routines [Non standard]

       A manual page consists of several sections.

       Conventional section names include  NAME,  SYNOPSIS,  CONFIGURA‐
       TION,  DESCRIPTION,  OPTIONS, EXIT STATUS, RETURN VALUE, ERRORS,
       ENVIRONMENT, FILES, VERSIONS, CONFORMING TO, NOTES, BUGS,  EXAM‐
       PLE, AUTHORS, and SEE ALSO.

       The  following conventions apply to the SYNOPSIS section and can
       be used as a guide in other sections.

       bold text          type exactly as shown.
       italic text        replace with appropriate argument.
       [-abc]             any or all arguments within [ ] are optional.
       -a|-b              options delimited by |  cannot  be  used  to‐
                          gether.
       argument ...       argument is repeatable.
       [expression] ...   entire expression within [ ] is repeatable.
```
We then run ```man -k challenge```
```

hacker@man~searching-for-manuals:~$ man -k challenge
cecztlgccg (1)       - print the flag!
hacker@man~searching-for-manuals:~$ man cecztlgccg

CHALLENGE(1)               Challenge Commands              CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --cecztl NUM
              print the flag if NUM is 029

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The   repository   for  this  dojo:  <https://github.com/pwncol‐
       lege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                     May 2024                   CHALLENGE(1)
```
And then finally run ```/challenge/challenge --cecztl 029```
```
hacker@man~searching-for-manuals:~$ /challenge/challenge --cecztl 029
Correct usage! Your flag: pwn.college{Qc0ecG2zMt-l9gYccgqbhhdosIp.dZTM4QDLygDO0czW}
```
## Helpful Programs 
Some programs don't have a man page, but we can learn how to run them by using ```--help```
or ```-h```.
In this level, we try reading a program's documentation with --help
```
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v]
                                            [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option
                        to give you the flag
hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 651
hacker@man~helpful-programs:~$ /challenge/challenge -g 651
Correct usage! Your flag: pwn.college{o6UgjdT5txqu1eUWgaaSXsUOS59.ddjM4QDLygDO0czW}
```
## Help for Builtins 
Some commands, rather than being programs with man pages and help options, are built into the shell itself. These are called builtins.
They can be invoked just like commands but its handled internally.
You can get a list of shell builtins by running the builtin help.
```hacker@dojo:~$ help```
In this challenge we first ```help challenge``` and then do as instructed.
```
hacker@man~help-for-builtins:~$ help challenge 
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!
    
    Options:
      --fortune		display a fortune
      --version		display the version
      --secret VALUE	prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "gyVxopTA".
hacker@man~help-for-builtins:~$ challenge --secret gyVxopTA
Correct! Here is your flag!
pwn.college{gyVxopTAkQJmp5UI51UMLmP7od8.dRTM5QDLygDO0czW}
```
Module 4 completed.


