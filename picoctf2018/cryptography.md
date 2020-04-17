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

