# Forensics 
## Scan Surprise 
In this challenge all i had to do was scan the popped up QR code to get the flag.
```
picoCTF{p33k_@_b00_3f7cf1ae}
```

<img width="434" alt="Screenshot 2024-11-07 at 3 34 51 PM" src="https://github.com/user-attachments/assets/9b05fb5d-01bf-41f0-bb27-f06e236d767c">

## Secret of the Polyglot
In this challenge upon downloading the pdf file and opening it i noticed it contained what looked at the second half of a flag.
But how do i get the first part?
I looked at the hint which said "This problem can be solved by just opening the file in different ways"
So did they mean not as a pdf?
This following was a happy accident. I converted the pdf to .png just to see what would happen. (i could always download the pdf again if it was wrong)
![flag2of2-final](https://github.com/user-attachments/assets/f4ef1e57-9867-495e-9c2c-d26a54190924)
However i got this.
So i combined the text in the picture and the text in the pdf to get the flag.
```
picoCTF{f1u3n7_1n_pn9_&_pdf_2a6a1ea8}
```
## CanYouSee
My first idea was to do what i had done in the oasisCTF.
But that didnt get me anywhere.
```
strings ukn_reality.jpg | grep picoCTF{
```


