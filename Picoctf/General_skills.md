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
