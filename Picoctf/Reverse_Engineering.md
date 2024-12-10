# Reverse_Engineering
## ARMssembly 1
Note: format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits)
Terms:
- str: store value in memory (str	w0, [sp, 12] stores the value of w0 at memory sp+12)
- ldr: load value from memory (ldr	w0, [sp, 20] #ldr loads value at sp+20)
- mov: move value into register (mov	w0, 3 #3 in w0)
- add: add values (add a b c a=b+c)
- sub: subtract values (sub a b c a=b-c)
- sdiv: divide values (sdiv a b c a=b/c
- lsl: shift bits left(lsl a b c a = b * (2^c))
- wzr: zero register (always 0).
- sp: stack pointer
```
func: #w 32 bit
	sub	sp, sp, #32
	str	w0, [sp, 12] # w0 holds a value which is stored at memory location sp+12 (say X)
	mov	w0, 81 # 81 in w0
	str	w0, [sp, 16] # now value at w0 (81) is at sp+16
	str	wzr, [sp, 20] #wzr holds 0 so 0 is saved at memory sp+20
	mov	w0, 3 #3 in w0
	str	w0, [sp, 24] #value at w0(3) is stored at memory sp+24
	ldr	w0, [sp, 20] #ldr loads value at sp+20 so Now w0=0(sp+20 held 0)
	ldr	w1, [sp, 16] #w1=81
	lsl	w0, w1, w0 #w0 is now 81 x 2^0 which is 81
	str	w0, [sp, 28] #w0 value (81) is stored at sp+28
	ldr	w1, [sp, 28] #w1 value(81) stored at sp+28
	ldr	w0, [sp, 24] #sp+24 value (3) is stored at w0
	sdiv	w0, w1, w0 #w0=81/3=27
	str	w0, [sp, 28] #w0 value (27) held at sp+28
	ldr	w1, [sp, 28] #w1 value = value at sp+28 which is 27
	ldr	w0, [sp, 12] # w0 now holds X
	sub	w0, w1, w0 #27-X=Y
	str	w0, [sp, 28] # w0=Y stored at sp+28
	ldr	w0, [sp, 28] Y
	add	sp, sp, 32
	ret
	.size	func, .-func
	.section	.rodata
	.align	3
```
```
sp+12=X
sp+16=81
sp+20=0
sp+24=3
sp+28=27

w0(sp+20)=0
w1(sp+16)=81
w0=81*2^0

w1=81(sp+28)
w0(sp+24)=3
w0=27

sp+28=27

w1(sp+28)=27
w0(sp+12)=X
w0=27-X(sp+28)
```
Looking at the main function <br>
```bne .L4``` branch not equal which refers to the fact that if ```cmp	w0, 0``` is not 0 it executes L4 but we want L0
So in order for w0 to be zero.
```w0=27-X(sp+28)``` X must be 27.
27 in hexadecimal 32 bit is ```0000001b```
Thus the flag is ```picoCTF{0000001b}```
