# File Globbing
## Matching with *
When the glob encounters a * character in any argument, the shell will treat it as "wildcard" and try to replace that argument with any files that match the pattern
```
hacker@globbing~matching-with-:~$ cd /c*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{AxT3Gwjpuiimgz6ddtDXXe3EjCT.dFjM4QDLygDO0czW}
```
we are restrained to keep the argument less than four characters.
Alternatively we can also use ```/ch*```.
## Matching with ?
When the glob encounters a ? character in any argument, the shell will treat it as single-character wildcard. This works like *, but only matches one character.
In this level we are asked to replace c and l with ?.
```
hacker@globbing~matching-with-:~$ cd /challenge
You used either the 'c', 'l', or '*' characters. Disallowed!
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{clc2T5ZqArgQ5C4OFECJO1rzNdI.dJjM4QDLygDO0czW}
```
In the first trial you can see what happens when you dont replace c l with ?
## Matching with []
The square brackes are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets.
For example [xyz] will match the character x, y, or z.
```
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{cK178VYa6tN-bVgQHeBmGOJtYZj.dNjM4QDLygDO0czW}
```
## Matching paths with []
Globbing happens on a path basis, so you can expand entire paths with your globbed arguments.
When i first attempted this i tried ```/challenge/run``` while still in ```/challenge/files``` directory.
Then upon reading the description again I realised that we had to run the challenge while still in home directory.
```
hacker@globbing~matching-paths-with-:~$ cd /challenge/files
hacker@globbing~matching-paths-with-:/challenge/files$ ls
file_a  file_d  file_g  file_j  file_m  file_p  file_s  file_v  file_y
file_b  file_e  file_h  file_k  file_n  file_q  file_t  file_w  file_z
file_c  file_f  file_i  file_l  file_o  file_r  file_u  file_x
hacker@globbing~matching-paths-with-:/challenge/files$ cd
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{0ky2KfOpu8CssXxEYheStrcHBT7.dRjM4QDLygDO0czW}
hacker@globbing~matching-paths-with-:~$ 
```
## Mixing globs
So we can combine globs.
```
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ ls
amazing      fantastic   kind        pwning     uplifting   zesty
beautiful    great       laughing    queenly    victorious
challenging  happy       magical     radiant    wonderful
delightful   incredible  nice        splendid   xenial
educational  jovial      optimistic  thrilling  youthful
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [ice]
Your expansion did not expand to the requested files (challenging, educational, 
pwning). Instead, it expanded to:
[ice]
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [ice]*
Your expansion did not expand to the requested files (challenging, educational, 
pwning). Instead, it expanded to:
challenging educational incredible
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{Y9kGG4FsEq-CUot0PKao_XZwTZK.dVjM4QDLygDO0czW}
```
Trial 1: I didnt combine anything, but it showed me an error.
Trial 2: I didnt realise that the letters i typed inside [] would return the files starting with the respective letters.
i thought it would show me the files with those letters present in them.
Trial 3: Once i realise the error in trial 2 trial 3 was simply ```[cep]*```
## Exclusionary globbing 
If the first character in the brackets is a !that bracket instance matches characters that aren't listed.
After reading the example provided figuring out the challenge was easy.
```
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{4NUl0v8DKf5mpRW9z5ISCFOMqiy.dZjM4QDLygDO0czW}
```
