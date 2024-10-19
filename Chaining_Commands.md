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

