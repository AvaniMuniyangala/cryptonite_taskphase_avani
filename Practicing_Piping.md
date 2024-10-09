# Practicing Piping
## Redirecting output
The syntax for redirecting files is ```hacker@dojo:~$ echo hi > asdf```
Using the syntax knowledge we can easily retrieve the flag.
```
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your 
flag:
pwn.college{chsa2J51RXXRy8xcxo7A-TLc9FP.dRjN1QDLygDO0czW}
```
## Redirecting more output 
In thsi challenge we are asked to redirect the output of ```/challenge/run``` to ```myflag```
```
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{I1QFxhsqgythkMPEsmN8wtURBk5.dVjN1QDLygDO0czW}

hacker@piping~redirecting-more-output:~$
```
When you do not do that this happens:
```
hacker@piping~redirecting-more-output:~$ /challenge/run
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[FAIL] You did not satisfy all the execution requirements.
[FAIL] Specifically, you must fix the following issue:
[FAIL]   You have not redirected anything for this process' stdout
```
## Appending output
You can redirect input in append mode using ```>>``` instead of ```>```.
```
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do 
the first write directly to the file, and the second write, I'll do to stdout 
(if it's pointing at the file). If you redirect the output in append mode, the 
second write will append to (rather than overwrite) the first write, and you'll 
get the whole flag!
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
 | 
\|/ This is the first half:
 v 
pwn.college{wkheVckcGeki6iRN0TLIJkm1gZ5.ddDM5QDLygDO0czW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>) 
rather than *append* mode (>>), and so the write of the second half to stdout 
overwrote the initial write of the first half directly to the file. Try append 
mode!
```
## Redirecting errors
In this challenge we have to redirect the output of /challenge/run to myflag, and then to instructions.
We will use ```/challenge/run > myflag 2> instructions```
```
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{QmRV4WqsHsolJEAH8hQ8mJRfS-y.ddjN1QDLygDO0czW}
```
## Redirecting input
You can redirect input to programs. This is done using ```<```.
```
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read 
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{8vdwp_vjalNWm5rd45buLJcp6aM.dBzN1QDLygDO0czW}
```
## Grepping stored results
In this level we put together the ```>``` and the ```grep``` command.
These are the instructiosn given to us <br>
1.Redirect the output of /challenge/run to /tmp/data.txt.<br>
2.This will result in a hundred thousand lines of text, with one of them being the flag, in /tmp/data.txt.<br>
3.Grep that for the flag!<br>
```
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep pwn.college ?tmp/data.txt
grep: ?tmp/data.txt: No such file or directory
hacker@piping~grepping-stored-results:~$ grep pwn.college /tmp/data.txt
pwn.college{w7qarq3XFFkezGuIvz4NMbGlu3c.dhTM4QDLygDO0czW}
```
## Grepping live output
When we use the pipe operator '|' the standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe.
```
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{cCWWtd10Y4Vy_0P7pxGIBbV_UgM.dlTM4QDLygDO0czW}
```
## Grepping errors
The shell has a >& operator, which redirects a file descriptor to another file descriptor.
First, we redirect standard error to standard output (2>& 1) and then pipe the now-combined stderr and stdout as normal (|).
```
hacker@piping~grepping-errors:~$ /challenge/run 2>& 1 | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{IzPtu2OqM7WoUVYM4ZYuKAdg4Zv.dVDM5QDLygDO0czW}
```
## Duplicating piped data with tee
The tee command, duplicates data flowing through your pipes to any number of files provided on the command line.
Looking at the example 
```
hacker@dojo:~$ echo hi | tee pwn college
hi
hacker@dojo:~$ cat pwn
hi
hacker@dojo:~$ cat college
hi
hacker@dojo:~$
```
We now better understand how ```tee``` works.
```
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee myflag | /challenge/college
Processing...
WARNING: you are overwriting file myflag with tee's output...
The input to 'college' does not contain the correct secret code! This code 
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the 
output of 'pwn' and figure out what the code needs to be.
hacker@piping~duplicating-piped-data-with-tee:~$ cat myflag
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "w0Q2IOKc"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret w0Q2IOKc | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{w0Q2IOKczqtzTUMHSLTYomgSAFn.dFjM5QDLygDO0czW}
```
## Writing to multiple programs 
In this challenge, we have /challenge/hack, /challenge/the, and /challenge/planet we are asked to run the /challenge/hack command, and duplicate its output as input to both the /challenge/the and the /challenge/planet commands.
We can use ```tee``` to duplicate data to two files and duplicate data to a file and a command.
When you write an argument of >(rev), bash will run the rev command, this command reads data from standard input, reverses its order, and writes it to standard output. It however hooks up its input to a temporary file that it will create. 
```
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack |tee >(/challenge/the) | /challenge/planet
Congratulations, you have duplicated data into the input of two programs! Here 
is your flag:
pwn.college{8wy2wnDhRTJmJGIPW974NdJ3foF.dBDO0UDLygDO0czW}
```
## Split-piping stderr and stdout
The | operator links the stdout of the left command with the stdin of the right command.
The 2>&1 operator to redirect stderr into stdout.
At the end of the description we are provided with the following information.<br>
In this challenge, you have:<br>
1./challenge/hack: this produces data on stdout and stderr<br>
2./challenge/the: you must redirect hack's stderr to this program<br>
3./challenge/planet: you must redirect hack's stdout to this program<br>
Using the above instructions
```
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack 2> >(/challenge/the) | /challenge/planet
Congratulations, you have learned a redirection technique that even experts 
struggle with! Here is your flag:
pwn.college{80-iftVz4b3w5SDnqxz8ICJGOlI.dFDNwYDLygDO0czW}
```
<br>
<br>
Module six completed.



