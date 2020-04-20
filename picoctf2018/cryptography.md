# Cryptography

### **HEEEEEEERE'S Johnny! - Points: 100**

* [Hints](https://2018game.picoctf.com/problems#72229da984df4634d538e93be00b9812hint)
  * If at first you don't succeed, try, try again. And again. And again.
  * If you're not careful these kind of problems can really "rockyou".

> Okay, so we found some important looking files on a linux computer. Maybe they can be used to get a password to the process. Connect with `nc 2018shell.picoctf.com 35225`. Files can be found here: [passwd](https://2018shell.picoctf.com/static/a488bb3c175bc843e0fbce95fff920d9/passwd) [shadow](https://2018shell.picoctf.com/static/a488bb3c175bc843e0fbce95fff920d9/shadow).

Download the file and run John the ripper on them to reveal the flag.

```text
poh@pohSurface:/mnt/d/pradagy/projects/ctf/pico2018$ john -show passwd 
0 password hashes cracked, 0 left
poh@pohSurface:/mnt/d/pradagy/projects/ctf/pico2018$ john -show shadow 
root:hellokitty:17770:0:99999:7:::
```

Then login using the credentials

```text
tokumeipoh@pico-2018-shell:~$ nc 2018shell.picoctf.com 35225
Username: root
Password: hellokitty
picoCTF{J0hn_1$_R1pp3d_99c35524}
```

### **caesar cipher 1 - Points: 150**

> This is one of the older ciphers in the books, can you decrypt the [message](https://2018shell.picoctf.com/static/6b5626c0736d9090f5d98de74eec4543/ciphertext)? You can find the ciphertext in /problems/caesar-cipher-1\_0\_931ac10f43e4d2ee03d76f6914a07507 on the shell server.

Used this site [https://www.dcode.fr/caesar-cipher](https://www.dcode.fr/caesar-cipher).   
picoCTF{justagoodoldcaesarcipherobyujeez}

### Hertz **- Points: 150**

> Here's another simple cipher for you where we made a bunch of substitutions. Can you decrypt it? Connect with `nc 2018shell.picoctf.com 18581`.  
> Hints: NOTE: Flag is not in the usual flag format

Once you login, you are shown a long text. Using this site, [https://quipqiup.com/](https://quipqiup.com/), helps solve the problem. I learned from this substitution type of cipher requires more data to be more accurate. E.g. when I only provided the header:

_zmtwkafo xlkl ro gmuk cpaw - ouiofrfufrmt\_zrnxlko\_akl\_ompvaipl\_zbrpwtbptn_

The site returned this:  
_congrats here is your flag - substitution\_ciphers\_are\_solvable\_c?ilgn?lnp_

But when i gave it more of the text:

_zmtwkafo xlkl ro gmuk cpaw - ouiofrfufrmt\_zrnxlko\_akl\_ompvaipl\_zbrpwtbptn  
---------------------------------------------------------------------------------------------------------------------------------  
ofaflpg, npuhn iuzd hupprwat zahl ckmh fxl ofarkxlab, ilakrtw a imyp mc pafxlk mt yxrzx a hrkkmk atb a kasmk pag zkmoolb. a glppmy bkloortwwmyt, utwrkbplb, yao ouofartlb wltfpg ilxrtb xrh mt fxl hrpb hmktrtw ark. xl xlpb fxl imyp apmcf atb rtfmtlb:_

The site returned this:  
_congrats here is your flag - substitution\_ciphers\_are\_solvable\_cdilgndlnp  
 -------------------------------------------------------------------------------   
stately, plump buck mulligan came from the stairhead, bearing a bowl of lather on which a mirror and a razor lay crossed. a yellow dressinggown, ungirdled, was sustained gently behind him on the mild morning air. he held the bowl aloft and intoned:_

picoCTF{_substitution\_ciphers\_are\_solvable\_cdilgndlnp}_

