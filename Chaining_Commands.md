# Chaining Commands
## Chaining with semicolons
The easiest way to chain commands is ```;```.
In this challenge all we had to do was chain ```/challenge/pwn``` and ```/challenge/college```
```
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{QXfcCw3mDKy_xBn7VHQw-rZz19f.dVTN4QDLygDO0czW}
```
## Your first shell script
As we combine more and more commands to achieve complex effects, the length of the combined prompt quickly gets really difficult to deal with. When this happens, we put these commands in a file, called a shell script, and run them by executing the file.
By convention, shell scripts are frequently named with a sh suffix
And then we can execute by passing it as an argument to a new instance of our shell (bash).
Trial 1
```
hacker@chaining~your-first-shell-script:~$ /challenge/pwn > x
It looks like you may have chained the pwn command with a pipe or other input 
redirection method. In this level, you must script the commands to run one 
after the other, without piping or redirection!
```
Trial 2
```
hacker@chaining~your-first-shell-script:~$ /challenge/pwn; /challenge/college > x
hacker@chaining~your-first-shell-script:~$ bash x.sh
You must first call the '/challenge/pwn' command, not 'trap dbg debug'!
```
Then i realised i was supposed to use ```echo```.
Trial 3
```
hacker@chaining~your-first-shell-script:~$ touch x.sh
hacker@chaining~your-first-shell-script:~$ echo /challenge/pwn; /challenge/college > x.sh
/challenge/pwn
```
Trial four is the charm?
```
hacker@chaining~your-first-shell-script:~$ echo "/challenge/pwn; /challenge/college" > x.sh
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{opUT-o6zpo3MKuDWxmTytMAlQc4.dFzN4QDLygDO0czW}
```
## Redirecting script output 
Reminder: > for stdout, 2> for stderr, < for stdin, >> and 2>> for append-mode redirection, >& for redirecting to other file descriptors, and | for piping to another command.
```
hacker@chaining~redirecting-script-output:~$ touch x.sh
hacker@chaining~redirecting-script-output:~$ echo "/challenge/pwn; /challenge/college" > x.sh
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{4Quhkl9RPXtJMuguKKv3GIAcvDz.dhTM5QDLygDO0czW}
```
## Executable shell scripts 
We can avoid the need to manually invoke bash. If your shell script file is executable.
```
hacker@chaining~executable-shell-scripts:~$ touch a.sh
hacker@chaining~executable-shell-scripts:~$ echo /challenge/solve > a.sh
hacker@chaining~executable-shell-scripts:~$ chmod ugo+x a.sh
hacker@chaining~executable-shell-scripts:~$ /a.sh
ssh-entrypoint: /a.sh: No such file or directory
hacker@chaining~executable-shell-scripts:~$ ./a.sh
Congratulations on your shell script execution! Your flag:
pwn.college{cvvum_S6vyoyy1TXe0lXk1fnTgR.dRzNyUDLygDO0czW}
```
Module 11 completed.



