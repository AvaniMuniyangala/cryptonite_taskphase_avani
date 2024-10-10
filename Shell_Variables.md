# Shell Variables
## Printing Variables 
You can print out variables with echo, by prepending the variable name with a $.
The syntax for printing variables.
```
hacker@dojo:~$ echo $PWD
/home/hacker
```
We can thus recieve the flag by printing the flag variable.
```
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{oj70fWOPi_StkNCOMJfmPcxEuKv.ddTN1QDLygDO0czW}
```
## Setting variables
We can set values to variables using ```=```

