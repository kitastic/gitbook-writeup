# General Skills



### **grep 1 - Points: 75 - \(Solves: 38278\)General Skills**

> Can you find the flag in [file](https://2018shell.picoctf.com/static/805ac70722810caa0b1c02bc88ef68d8/file)? This would be really obnoxious to look through by hand, see if you can find a faster way. You can also find the file in /problems/grep-1\_0\_c0c0c16438cdbee39591397e16389f59 on the shell server.

```bash
tokumeipoh@pico-2018-shell:/problems/grep-1_0_c0c0c16438cdbee39591397e16389f59$ cat file | grep "picoCTF{"
picoCTF{grep_and_you_will_find_52e63a9f}
```

### **net cat - Points: 75 - \(Solves: 33835\)General Skills**

> Using netcat \(nc\) will be a necessity throughout your adventure. Can you connect to `2018shell.picoctf.com` at port `22847` to get the flag?

```text
tokumeipoh@pico-2018-shell:~$ nc 2018shell.picoctf.com 22847
That wasn't so hard was it?
picoCTF{NEtcat_iS_a_NEcESSiTy_69222dcc}
```



**strings - Points: 100 - \(Solves: 24664\)General Skills**

> Can you find the flag in this [file](https://2018shell.picoctf.com/static/e78981e684a62559baaef12a27f0e918/strings) without actually running it? You can also find the file in /problems/strings\_0\_bf57524acf558aca2081eb97ece8e2ee on the shell server.

### 

Using strings alone will show too much information in terminal, therefore, use grep also to find flag.

```text
tokumeipoh@pico-2018-shell:~$ strings /problems/strings_0_bf57524acf558aca2081eb97ece8e2ee/strings | grep 
"picoCTF{"
picoCTF{sTrIngS_sAVeS_Time_c09b1444}
```

**pipe - Points: 110 - \(Solves: 22857\)General Skills**

> During your adventure, you will likely encounter a situation where you need to process data that you receive over the network rather than through a file. Can you find a way to save the output from this program and search for the flag? Connect with `2018shell.picoctf.com 2015`

```text
tokumeipoh@pico-2018-shell:~$ nc 2018shell.picoctf.com 2015 | grep "picoCTF{"
picoCTF{almost_like_mario_8861411c}
```

**Inspect Me - Points: 125 - \(Solves: 29304\)Web Exploitation**

> Inpect this code! `http://2018shell.picoctf.com:56252` \([link](http://2018shell.picoctf.com:56252/)\)

Load the page in browser and start developer tools with ctrl+shift+i. Under sources tab, in main folder called 2018shell.picoctf.com:56252 will be 3 files.   
\(index\) at line 31 is 1/3 of flag: picoCTF{ur\_4\_real\_1nspe  
mycss.css at line 51 is 2/3 of flag: ct0r\_g4dget\_9dd3b33c}  
3/3 of flag is not really needed because we already have completed flag.

**grep 2 - Points: 125 - \(Solves: 21273\)General Skills**

> This one is a little bit harder. Can you find the flag in /problems/grep-2\_2\_413a577106278d0711d28a98f4f6ac28/files on the shell server? Remember, grep is your friend.

```text
tokumeipoh@pico-2018-shell:/problems/grep-2_2_413a577106278d0711d28a98f4f6ac28/files$ ll
total 48
drwxr-xr-x 12 root root 4096 Mar 25  2019 ./     
drwxr-xr-x  3 root root 4096 Mar 25  2019 ../    
drwxr-xr-x  2 root root 4096 Mar 25  2019 files0/
drwxr-xr-x  2 root root 4096 Mar 25  2019 files1/
drwxr-xr-x  2 root root 4096 Mar 25  2019 files2/
drwxr-xr-x  2 root root 4096 Mar 25  2019 files3/
drwxr-xr-x  2 root root 4096 Mar 25  2019 files4/
drwxr-xr-x  2 root root 4096 Mar 25  2019 files5/
drwxr-xr-x  2 root root 4096 Mar 25  2019 files6/
drwxr-xr-x  2 root root 4096 Mar 25  2019 files7/
drwxr-xr-x  2 root root 4096 Mar 25  2019 files8/
drwxr-xr-x  2 root root 4096 Mar 25  2019 files9/
tokumeipoh@pico-2018-shell:/problems/grep-2_2_413a577106278d0711d28a98f4f6ac28/files$ grep -r "picoCTF{" 
../files5/file24:picoCTF{grep_r_and_you_will_find_8eb84049}
```

**Aca-Shell-A - Points: 150 - \(Solves: 18373\)General Skills**

> It's never a bad idea to brush up on those linux skills or even learn some new ones before you set off on this adventure! Connect with `nc 2018shell.picoctf.com 33158`.

This challenge is timed! It seems like you are interactive with an AI within the terminal.   
1. you have to delete all files in "secret" folder  
2. go into executables folder to retrieve and run exploit file  
3. you will be prompted to copy a file from the tmp folder to passwords folder and then view the file

```bash
Sweet! We have gotten access into the system but we aren't root.
It's some sort of restricted shell! I can't see what you are typing
but I can see your output. I'll be here to help you along.
If you need help, type "echo 'Help Me!'" and I'll see what I can do
There is not much time left!
~/$ cd secret
Now we are cookin'! Take a look around there and tell me what you find!
~/secret$ ls
intel_1
intel_2
intel_3
intel_4
intel_5
profile_ahqueith5aekongieP4ahzugi
profile_ahShaighaxahMooshuP1johgo
profile_aik4hah9ilie9foru0Phoaph0
profile_AipieG5Ua9aewei5ieSoh7aph
profile_bah9Ech9oa4xaicohphahfaiG
profile_ie7sheiP7su2At2ahw6iRikoe
profile_of0Nee4laith8odaeLachoonu
profile_poh9eij4Choophaweiwev6eev
profile_poo3ipohGohThi9Cohverai7e
profile_Xei2uu5suwangohceedaifohs
Sabatoge them! Get rid of all their intel files!
~/secret$ rm intel*
Nice! Once they are all gone, I think I can drop you a file of an exploit!
Just type "echo 'Drop it in!' " and we can give it a whirl!
~/secret$ echo "drop it in!"
Drop it in!
I placed a file in the executables folder as it looks like the only place we can execute from!
Run the script I wrote to have a little more impact on the system!
~/secret$ cd ..
~/$ cd executables
~/executables$ ls
dontLookHere
~/executables$ ./dontLookHere          
 d940 ecc3 9426 5624 2976 8abf 7cf1 2d8e 32b0 063b 2f48 44c9 d9cb efad b644 a481 3e24 0536 7b7e dcf8 c2c2
b4db 0c21 3b0c 6881
 94eb 4e23 3918 086d 09b7 1935 8547 ee90 4ddd 2e61 845a b19f d09a 3419 c1dc c74e f2a7 c29e 971e 3342 5d3f
5b21 1397 373b ece3
.
.
.
  3376 28be a382 4dbe dd95 8686 4725 561c 6476 7dea a804 5eed 980a 4080 6319 758c d616 3aa1 c108 26ac e6c2
a2a8 2e7f fb5c 6025
 2e32 11ca 772f 52d7 bbf5 359c 5f32 3b91 d03a 34ef 41d9 30fc 1186 1f6c b6c0 6d57 fb76 9238 45e7 5755 c4d7
a052 aa36 75f8 8b77
Looking through the text above, I think I have found the password. I am just having trouble with a usernae.
Oh drats! They are onto us! We could get kicked out soon!
Quick! Print the username to the screen so we can close are backdoor and log into the account directly!
You have to find another way other than echo!
~/executables$ whoami
l33th4x0r
Perfect! One second!
Okay, I think I have got what we are looking for. I just need to to copy the file to a place we can read.
Try copying the file called TopSecret in tmp directory into the passwords folder.
~/executables$ cd ..
~/$ cp /tmp/TopSecret passwords
~/$ cd passwords
~/passwords$ ls
TopSecret
~/passwords$ cat TopSecret
Major General John M. Schofield's graduation address to the graduating class of 1879 at West Point is as follows: The discipline which makes the soldiers of a free country reliable in battle is not to be gained by harlh or tyrannical treatment.On the contrary, such treatment is far more likely to destroy than to make an army.It is possible to impart instruction and give commands in such a manner and such a tone of voice as to insplows: The discipline which makes the soldiers of a free country reliable in battle is not to be gained by hnot fail to excite strong resentment and a desire to disobey.The one mode or other of dealing with subordinatea springs from a corresponding spirit in the breast of the commander.He who feels the respect which is due to others, cannot fail to inspire in them respect for himself, while he who feels,and hence manifests disrespe~/$ cd passwords~/passwords$ lsTopSecret~/passwords$ cat TopSecretMajor General John M. Schofield's graduation address to the graduating class of 1879 at West Point is as follows: The discipline which makes the soldiers of a free country reliable in battle is not to be gained by 
harsh or tyrannical treatment.On the contrary, such treatment is far more likely
```

