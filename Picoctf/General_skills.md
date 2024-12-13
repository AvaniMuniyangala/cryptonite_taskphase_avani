# General skills 
## Binary search 
Okay this challenge was pretty easy i still did go through the hints to make the flag finding process faster.
All we are required to do is guess the randomly generated number and the flag is handed to us.
```
Welcome to the Binary Search Game!
I'm thinking of a number between 1 and 1000.
Enter your guess: 500
Lower! Try again.
Enter your guess: 350
Lower! Try again.
Enter your guess: 150
Higher! Try again.
Enter your guess: 250
Lower! Try again.
Enter your guess: 200
Higher! Try again.
Enter your guess: 235
Congratulations! You guessed the correct number: 235
Here's your flag: picoCTF{g00d_gu355_3af33d18}
Connection to atlas.picoctf.net closed.

```
## Verify 
This challenge was easy though most of the errors i made were syntax and typos.
Took me an unnaturally long time to realise why it wouldnt work.
I did however refer to the hints.
```
ctf-player@pico-chall$ ls
checksum.txt  decrypt.sh  files
ctf-player@pico-chall$ cat checksum.txt
5848768e56185707f76c1d74f34f4e03fb0573ecc1ca7b11238007226654bcda
ctf-player@pico-chall$ sha files/* | greap "5848768e56185707f76c1d74f34f4e03fb0573ecc1ca7b11238007226654bcda"
-bash: greap: command not found
-bash: sha: command not found
ctf-player@pico-chall$ sha files/* | grap "5848768e56185707f76c1d74f34f4e03fb0573ecc1ca7b11238007226654bcda"
-bash: grap: command not found
-bash: sha: command not found
ctf-player@pico-chall$ sha files/* | grep "5848768e56185707f76c1d74f34f4e03fb0573ecc1ca7b11238007226654bcda"
-bash: sha: command not found
ctf-player@pico-chall$ sha256sum files/* | grep "5848768e56185707f76c1d74f34f4e03fb0573ecc1ca7b11238007226654bcda"
5848768e56185707f76c1d74f34f4e03fb0573ecc1ca7b11238007226654bcda  files/8eee7195
ctf-player@pico-chall$ cat files/8eee7195
Salted__??^?&ߴ?a??b??d
??ZS?@???퀶 xT?	JU?xoZ?U-?Z???QF9ոctf-player@pico-chall$ ./decrypt.sh files/8eee7195
picoCTF{trust_but_verify_8eee7195}
```
## ASCII Numbers 
- hint 1 : CyberChef is a great tool for any encoding but especially ASCII.
- hint 2 : Try CyberChef's 'From Hex' function
<img width="1280" alt="Screenshot 2024-12-10 at 5 25 50 PM" src="https://github.com/user-attachments/assets/82877508-1b1b-4914-b1b5-b7fdab326371">
<br>

```picoCTF{45c11_n0_qu35710n5_1ll_t311_y3_n0_l135_445d4180}```

## useless
Once i connected it was a simple revision of linux 
```
picoplayer@challenge:~$ ls
useless
picoplayer@challenge:~$ cat useless
#!/bin/bash
# Basic mathematical operations via command-line arguments

if [ $# != 3 ]
then
  echo "Read the code first"
else
        if [[ "$1" == "add" ]]
        then 
          sum=$(( $2 + $3 ))
          echo "The Sum is: $sum"  

        elif [[ "$1" == "sub" ]]
        then 
          sub=$(( $2 - $3 ))
          echo "The Substract is: $sub" 

        elif [[ "$1" == "div" ]]
        then 
          div=$(( $2 / $3 ))
          echo "The quotient is: $div" 

        elif [[ "$1" == "mul" ]]
        then
          mul=$(( $2 * $3 ))
          echo "The product is: $mul" 

        else
          echo "Read the manual"
         
        fi
fi
picoplayer@challenge:~$ man useless

useless
     useless, -- This is a simple calculator script

SYNOPSIS
     useless, [add sub mul div] number1 number2

DESCRIPTION
     Use the useless, macro to make simple calulations like addition,subtraction, multiplication and division.

Examples
     ./useless add 1 2
       This will add 1 and 2 and return 3

     ./useless mul 2 3
       This will return 6 as a product of 2 and 3

     ./useless div 6 3
       This will return 2 as a quotient of 6 and 3

     ./useless sub 6 5
       This will return 1 as a remainder of substraction of 5 from 6

Authors
     This script was designed and developed by Cylab Africa

     picoCTF{us3l3ss_ch4ll3ng3_3xpl0it3d_5136}
```
## Magikarp Ground Mission
Challenge requires us to know cd cat and ls commands on bash.
```
ctf-player@pico-chall$ ls
1of3.flag.txt  instructions-to-2of3.txt
ctf-player@pico-chall$ cat instructions-to-2of3.txt
Next, go to the root of all things, more succinctly `/`
ctf-player@pico-chall$ cat 1of3.flag.txt
picoCTF{xxsh_
ctf-player@pico-chall$ cd /
ctf-player@pico-chall$ ls 
2of3.flag.txt  dev   instructions-to-3of3.txt  media  proc  sbin  tmp
bin            etc   lib                       mnt    root  srv   usr
boot           home  lib64                     opt    run   sys   var
ctf-player@pico-chall$ cat 2of3.flag.txt
0ut_0f_\/\/4t3r_
ctf-player@pico-chall$ cat instructions-to-3of3.txt
Lastly, ctf-player, go home... more succinctly `~`
ctf-player@pico-chall$ cd ~
ctf-player@pico-chall$ ls
3of3.flag.txt  drop-in
ctf-player@pico-chall$ cat 3of3.flag.txt
1118a9a4}
ctf-player@pico-chall$ cat drop-in
cat: drop-in: Is a directory
ctf-player@pico-chall$ cd drop-in
ctf-player@pico-chall$ ls
1of3.flag.txt  instructions-to-2of3.txt
```
FLAG: ```picoCTF{xxsh_0ut_0f_\/\/4t3r_1118a9a4}```

## Obedient Cat
Fastest solve ever.
I got the flag after downloading the file.
```picoCTF{s4n1ty_v3r1f13d_1a94e0f9}```

## First Grep
I found the flag skimming while skimming through the file.
However still used grep command to find the flag.
FLAG: ```picoCTF{grep_is_good_to_find_things_dba08a45}```
