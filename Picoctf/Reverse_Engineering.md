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

## vault-door-training
LEVEL: EASY <br>
The challenge introduces us to java code.<br>
We are presented with this program 
```
import java.util.*;

class VaultDoorTraining {
    public static void main(String args[]) {
        VaultDoorTraining vaultDoor = new VaultDoorTraining();
        Scanner scanner = new Scanner(System.in); 
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
	}
   }

    // The password is below. Is it safe to put the password in the source code?
    // What if somebody stole our source code? Then they would know what our
    // password is. Hmm... I will think of some ways to improve the security
    // on the other doors.
    //
    // -Minion #9567
    public boolean checkPassword(String password) {
        return password.equals("w4rm1ng_Up_w1tH_jAv4_eec0716b713");
    }
}
```
The flag was simply ```w4rm1ng_Up_w1tH_jAv4_eec0716b713``` wrapped in picoCTF{}. <br>
```picoCTF{w4rm1ng_Up_w1tH_jAv4_eec0716b713}```

## Vault door 1 
LEVEL: MEDIUM 
The challnege was straightforward. Just took some extra effort.
```
 password.length() == 32 &&
               password.charAt(0)  == 'd' &&
               password.charAt(29) == '3' &&
               password.charAt(4)  == 'r' &&
               password.charAt(2)  == '5' &&
               password.charAt(23) == 'r' &&
               password.charAt(3)  == 'c' &&
               password.charAt(17) == '4' &&
               password.charAt(1)  == '3' &&
               password.charAt(7)  == 'b' &&
               password.charAt(10) == '_' &&
               password.charAt(5)  == '4' &&
               password.charAt(9)  == '3' &&
               password.charAt(11) == 't' &&
               password.charAt(15) == 'c' &&
               password.charAt(8)  == 'l' &&
               password.charAt(12) == 'H' &&
               password.charAt(20) == 'c' &&
               password.charAt(14) == '_' &&
               password.charAt(6)  == 'm' &&
               password.charAt(24) == '5' &&
               password.charAt(18) == 'r' &&
               password.charAt(13) == '3' &&
               password.charAt(19) == '4' &&
               password.charAt(21) == 'T' &&
               password.charAt(16) == 'H' &&
               password.charAt(27) == 'f' &&
               password.charAt(30) == 'b' &&
               password.charAt(25) == '_' &&
               password.charAt(22) == '3' &&
               password.charAt(28) == '6' &&
               password.charAt(26) == 'f' &&
               password.charAt(31) == '0';
```
All we had to do was place the characters at their index postions.
We arrive at this <br>
```
d35cr4mbl3_tH3_cH4r4cT3r5_ff63b0
```
The flag : ```picoCTF{d35cr4mbl3_tH3_cH4r4cT3r5_ff63b0}```
