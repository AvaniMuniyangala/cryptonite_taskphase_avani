# Processes and Jobs
## Listing processes 
We can list running processes using the ```ps``` command.
```ps``` either stands for "process snapshot" or "process status", and it lists processes. <br>
Standard" Syntax: You can use``` -e``` to list every process and ```-f``` for a full format output, including arguments. These can be combined into a single argument ```-ef```.<br>
BSD Syntax: In this syntax, you can use ```a``` to list processes for all users,``` x``` to list processes that aren't running in a terminal, and ```u ```for a "user-readable" output. These can be combined into a single argument ```aux```.
```
hacker@processes~listing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  1 06:34 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 06:34 ?        00:00:00 /run/dojo/bin/sleep 6h
root          68       1  0 06:34 ?        00:00:00 /challenge/1985-run-6748
root          72      68  0 06:34 ?        00:00:00 sleep 6h
hacker        73       0  1 06:34 pts/0    00:00:00 /run/dojo/bin/ssh-entrypoint
hacker        91      73  0 06:34 pts/0    00:00:00 ps -ef
hacker@processes~listing-processes:~$ /challenge/1985-run-6748
Yahaha, you found me! Here is your flag:
pwn.college{0_3BkZ-iyIifDrP6WMcphapwu4Q.dhzM4QDLygDO0czW}
Now I will sleep for a while (so that you could find me with 'ps').
```
## Killing Processes 
```kill``` will terminate a process in a way that gives it a chance to get its affairs in order before ceasing to exist.
```
hacker@processes~killing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 06:36 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/pro
root           7       1  0 06:36 ?        00:00:00 /run/dojo/bin/sleep 6h
root          71       1  0 06:36 ?        00:00:00 su -c /challenge/.launcher hacker
hacker        73      71  0 06:36 ?        00:00:00 /challenge/dont_run
hacker        74      73  0 06:36 ?        00:00:00 sleep 6h
hacker        75       0  0 06:36 pts/0    00:00:00 /run/dojo/bin/ssh-entrypoint
hacker        94      75  0 06:37 pts/0    00:00:00 ps -ef
hacker@processes~killing-processes:~$ kill 73
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{EtnmxtqWKSAlYu9Wqktx3V-B66R.dJDN4QDLygDO0czW}
```
First we use ```ps -ef``` to find the processes being run currently. Then we find out that the PID code for ```/challenge/dont_run``` is 73.
So we then ```kill 73```.
And then ```/challenge/run```.
## Interrupting Processes 
We can interrupt a process by holding down on ```ctrl+c```.
```
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember, 
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{w8YfryAZ6yzJ1G_6m-blQsAYAQZ.dNDN4QDLygDO0czW}
```
In this challenge we were asked to ```/challenge/run``` and then interrupt said process by holding down on ```ctrl+c```.
## Suspending processes 
Instead of intrrupting we can also suspend processes using ```ctrl+z```.
First we ```/challenge/run```
```
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          85      65  0 06:43 pts/0    00:00:00 bash /challenge/run
root          87      85  0 06:43 pts/0    00:00:00 ps -f

I don't see a second me!
```
Then we suspend the process by ```ctrl+z```.
```
To pass this level, you need to suspend me and launch me again! You can 
background me with Ctrl-Z or, if you're not ready to do that for whatever 
reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
```
We then ```challenge/run``` again.
```
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          85      65  0 06:43 pts/0    00:00:00 bash /challenge/run
root          92      65  0 06:43 pts/0    00:00:00 bash /challenge/run
root          94      92  0 06:43 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{oEASU4Y0MCWSm2FiDeB545pl2Fj.dVDN4QDLygDO0czW}
```
## Resume processes
If you're going to suspend processes you have to resume them at some point.
```fg``` command is used to resume processes.

In this challenge we need to first run it, suspend and then resume to receve the flag.
```
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with 
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg
/challenge/run
I'm back! Here's your flag:
pwn.college{YO5spWlEqyWy8_WK1St3wy3HnDQ.dZDN4QDLygDO0czW}
Don't forget to press Enter to quit me!

Goodbye!
```
## Backgrounding Processes 
We can have processes running in the background and foreground.
we use ```bg``` for backgrounding a process and ```fg``` to forward it.
In this challenge we are asked to run a challenge suspend it to the backgorund and run it again.
```
hacker@processes~backgrounding-processes:~$ /challenge/run 
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S+   bash /challenge/run
root          84 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the 
background, and then launch a new version of me! You can background me with 
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to 
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ bg
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out.
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S    bash /challenge/run
root          92 S    sleep 6h
root          93 S+   bash /challenge/run
root          95 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{0B2nQBNNKSE3ccR9E-ICTZMdFKR.ddDN4QDLygDO0czW}
```
## Forwarding processes 
Well now that we put it in the background we use ```fg``` to bring it to the foreground.
In this challenge we run the challenge suspend it to the background and keep it running there and bring it to the foreground using ```fg```.

```
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the 
background, and *then* foreground it without re-suspending it! You can 
background me with Ctrl-Z (and resume me in the background with 'bg') or, if 
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~foregrounding-processes:~$ bg
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out. After that, resume me into the foreground with 'fg'; 
I'll wait.
hacker@processes~foregrounding-processes:~$ fg
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!
pwn.college{8LoLG8tYxVweXD2-FObmCQlayOd.dhDN4QDLygDO0czW}

```
## Starting background processes 
Background processes can be started using ```&```
In this challenge all we had to do was start /challenge/run in the background .
```
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 82



Yay, you started me in the background! Because of that, this text will probably 
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{0eITNttz4Nfyy82ClZ55lWZZ2b0.dlDN4QDLygDO0czW}
[1]+  Done                    /challenge/run
```
## Process exit codes 
We can access the exit code of the most recently-terminated command using the special ? variable. Prepending it with $ gives us the value 
```
hacker@processes~process-exit-codes:~$ /challenge/get-code
Exiting with an error code!
hacker@processes~process-exit-codes:~$ echo $?
41
hacker@processes~process-exit-codes:~$ /challenge/submit-code 41
CORRECT! Here is your flag:
pwn.college{UTWQR6SLFkxTi_rQgnp-Dub8uPO.dljN4UDLygDO0czW}
```
MODULE EIGHT!!!




