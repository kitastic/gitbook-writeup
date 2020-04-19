# Forensics

### **Desrouleaux - Points: 150**

> Our network administrator is having some trouble handling the tickets for all of of our incidents. Can you help him out by answering all the questions? Connect with `nc 2018shell.picoctf.com 10493`. [incidents.json](https://2018shell.picoctf.com/static/8eed8b873d59e897ae9dea0af40491f3/incidents.json)  
> [Hints](https://2018game.picoctf.com/problems#56af5d7b6c8f82e80205ecd9c9d66653hint): If you need to code, python has some good libraries for it.

Once connected the server will ask you three questions related to the json file.

> 1\) What is the most common source IP address? If there is more than one IP address that is the most common, you may give any of the most common ones.   
> 2\) How many unique destination IP addresses were targeted by the source IP address   
> 3\) What is the average number of unique destination IP addresses that were sent a file with the same hash? Your answer needs to be correct to 2 decimal places.

\***Note**\* _The answer to these questions vary depending on which port you connect to picoctf server._  
1\) Keep count of source IP.  
2\) \***Note**\* _The source IP might change with different attempts!_ For that source IP count how many unique destination IP exists.  
3\) This question is a bit tricky. It asks for each hash, what is the probabiilty that it will have unique destination IPs. Even though all hashes have two dst\_ip, but sometimes those dst\_ip are also sent a file with another hash, and therefore, not unique. 

The following is a python code written to answer these questions. Just input the question and it will show you the answer.

```python
'''
This code is meant to answer these questions from picoctf2018: Desouleaux challenge

What is the most common source IP address? If there is more than one IP address that is the most common, you may give any of the most common ones.

How many unique destination IP addresses were targeted by the source IP address 99.32.28.173?

What is the average number of unique destination IP addresses that were sent a file with the same hash? Your answer needs to be correct to 2 decimal places.
'''

import json
# Counter keeps count of occurences in a dictionary { "key": #}
from collections import Counter
# single key to multiple values
from collections import defaultdict
import re # regex

# have to open file first then load json
with open("incidents.json") as inc:
    incidents = json.load(inc)
    
questionsRemaining = 3
while (questionsRemaining > 0):
    question = input("Enter question {} of 3: ".format(questionsRemaining))
    if question.startswith("What is the most common source IP address"):
        # most common source IP, Counter keeps count of instances
        src_ip = Counter()  
        # iterate through each incident and count common source IP
        for incident in incidents["tickets"]:
            # cache each incident's information
            _src_ip = incident["src_ip"]            
            src_ip[_src_ip] += 1
        # src_ip = sorted(src_ip) alone will not work, must have lambda
        src_ip = sorted(src_ip, key=lambda i: i[0])
        print(src_ip[0])
    elif question.startswith("How many unique destination IP addresses"):
        # find src ip address within question
        ip = re.findall("\d+\.\d+.\d+.\d+", question)[0]
        # use set to discard duplicates
        dst_ip = set()
        # iterate through each incident
        for incident in incidents["tickets"]:
            _src_ip = incident["src_ip"]
            # if current ticket's src_ip matches search criteria, add it's dst_ip
            if _src_ip == ip:
                dst_ip.add(incident["dst_ip"])
        print(len(dst_ip))
    else:
        hashes = defaultdict(set)
        for incident in incidents["tickets"]:
            _hash = incident["file_hash"]
            _dst_ip = incident["dst_ip"]
            hashes[_hash].add(_dst_ip)
        # count how many unique dst_ip for all hashes
        UniqueDstIp = 0
        TotalHashes = len(hashes)
        for key, values in hashes.items():
            # print(f"{key} - {values}")
            # each hash may have multiple values
            UniqueDstIp += len(values)
        print(f"unique dst ip / total hashes = {UniqueDstIp} / {TotalHashes} = \
              \n {UniqueDstIp/TotalHashes}") 
        
            
    questionsRemaining -= 1      
```

```bash
You'll need to consult the file `incidents.json` to answer the following questions.


What is the most common source IP address? If there is more than one IP address that is the most common, you may give any of the most common ones.
251.71.156.29
Correct!


How many unique destination IP addresses were targeted by the source IP address 31.13.251.15?
2
Correct!


What is the number of unique destination ips a file is sent, on average? Needs to be correct to 2 decimal 
places.
1.125
Correct!


Great job. You've earned the flag: picoCTF{J4y_s0n_d3rUUUULo_a062e5f8}
```

**Reading Between the Eyes - Points: 150**

> Stego-Saurus hid a message for you in this [image](https://2018shell.picoctf.com/static/9129761dbc4bf494c47429f85ddf7434/husky.png), can you retreive it?  
> Hint: maybe you can find an online decoder?

I couldnt get [https://stylesuxx.github.io/steganography/](https://stylesuxx.github.io/steganography/) to work so I had to use zsteg.  
If Ruby is not installed in your linux: `sudo apt-get install ruby-full`  
Install zsteg instructions here [https://github.com/zed-0xff/zsteg](https://github.com/zed-0xff/zsteg)

```bash
poh@pohSurface:/mnt/d/pradagy/projects/ctf/pico2018$ zsteg husky.png 
/usr/lib/ruby/2.5.0/open3.rb:199: warning: Insecure world writable dir /home/poh/.local/bin in PATH, mode 
040777
b1,r,lsb,xy         .. text: "^5>c[rvyzrf@"
b1,rgb,lsb,xy       .. text: "picoCTF{r34d1ng_b37w33n_7h3_by73s}"
b1,abgr,msb,xy      .. file: PGP\011Secret Sub-key -
b2,g,msb,xy         .. text: "ADTU@PEPA"
b3,abgr,msb,xy      .. text: "t@Wv!Wt\tGtA"
b4,r,msb,xy         .. text: "0Tt7F3Saf"
b4,g,msb,xy         .. text: "2g'uV `3"
b4,b,lsb,xy         .. text: "##3\"TC%\"2f"
b4,b,msb,xy         .. text: " uvb&b@f!"
b4,rgb,lsb,xy       .. text: "1C5\"RdWD"
b4,rgb,msb,xy       .. text: "T E2d##B#VuQ`"
b4,bgr,lsb,xy       .. text: "A%2RTdGG"
b4,bgr,msb,xy       .. text: "EPD%4\"c\"#CUVqa "
b4,rgba,lsb,xy      .. text: "?5/%/d_tO"
b4,abgr,msb,xy      .. text: "EO%O#/c/2/C_e_q"
```

**Recovering From the Snap - Points: 150**

> There used to be a bunch of [animals](https://2018shell.picoctf.com/static/1603334c6d1519a49283974d0d480ffe/animals.dd) here, what did Dr. Xernon do to them?  
> Hint: Some files have been deleted from the disk image, but are they really gone?

 DD file is a [disk image](https://www.whatisfileextension.com/disk-image/) file and replica of a hard disk drive. The file having extension .dd is usually created with an imaging tool called DD. The utility provides command line interface to create disk images in a system running UNIX & LINUX OS. [\[info\]](https://www.whatisfileextension.com/dd/)

7zip can actually extract the .dd file. Install: `sudo apt install p7zip-full p7zip-rar` [\[info\]](https://www.tecmint.com/7zip-command-examples-in-linux/)

```bash
# 7z extract animals.dd 
# -oanimal means setting specified output directory named "animal"
poh@pohSurface:/mnt/d/pradagy/projects/ctf/pico2018$ 7z e animals.dd -oanimal

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=C.UTF-8,Utf16=on,HugeFiles=on,64 bits,8 CPUs Intel(R) Core(TM) i7-8650U CPU @ 
1.90GHz (806EA),ASM,AES-NI)

Scanning the drive for archives:
1 file, 10485760 bytes (10 MiB)

Extracting archive: animals.dd
--
Path = animals.dd
Type = FAT
Physical Size = 10485760
File System = FAT16
Cluster Size = 2048
Free Space = 8706048
Headers Size = 37376
Sector Size = 512
ID = 2607173086

Everything is Ok

Files: 4
Size:       1736281
Compressed: 10485760
```

4 images are extracted from the drive, but according to the hint, we need to dig deeper with `foremost` . Foremost is a forensic data recovery program for Linux used to recover files using their headers, footers, and data structures through a process known as file carving. To install:  
 `sudo apt install foremost`

```bash
poh@pohSurface:/mnt/d/pradagy/projects/ctf/pico2018$ foremost -v -o animals_foremost animals.dd
Foremost version 1.5.7 by Jesse Kornblum, Kris Kendall, and Nick Mikus
Audit File

Foremost started at Sat Apr 18 16:29:07 2020
Invocation: foremost -v -o animals_foremost animals.dd
Output directory: /mnt/d/pradagy/projects/ctf/pico2018/animals_foremost
Configuration file: /etc/foremost.conf
Processing: animals.dd
|------------------------------------------------------------------
File: animals.dd
Start: Sat Apr 18 16:29:07 2020
Length: 10 MB (10485760 bytes)

Num      Name (bs=512)         Size      File Offset     Comment

0:      00000077.jpg         617 KB           39424
1:      00001313.jpg         481 KB          672256
2:      00002277.jpg         380 KB         1165824
3:      00003041.jpg         248 KB         1556992
4:      00003541.jpg         314 KB         1812992
5:      00004173.jpg         458 KB         2136576
6:      00005093.jpg         383 KB         2607616
7:      00005861.jpg          39 KB         3000832
*|
Finish: Sat Apr 18 16:29:07 2020

8 FILES EXTRACTED

jpg:= 8
------------------------------------------------------------------

Foremost finished at Sat Apr 18 16:29:07 2020
```

This time you see more images are found in the animals\_foremost folder and 00005861.jpg shows the flag.  picoCTF{th3\_5n4p\_happ3n3d}

**admin panel - Points: 150**

> We captured some [traffic](https://2018shell.picoctf.com/static/162c41cc965c3db31c3acffecc3b2c87/data.pcap) logging into the admin panel, can you find the password?  
> Hint: Tools like wireshark are pretty good for analyzing pcap files.

Open the pcap file with wireshark. You can filter the list for http and browse around. To get the flag go to File &gt; Export Objects &gt; HTTP ... and choose save all. Then cat each file until you see the flag

```text
poh@pohSurface:/mnt/d/pradagy/projects/ctf/pico2018/admin panel$ ll
total 36
-rwxrwxrwx 1 poh poh  2149 Apr 18 16:53  %5c*
-rwxrwxrwx 1 poh poh  2149 Apr 18 16:53 '%5c(2)'*
drwxrwxrwx 1 poh poh  4096 Apr 18 16:53  ./
drwxrwxrwx 1 poh poh  4096 Apr 18 16:39  ../
-rwxrwxrwx 1 poh poh  1944 Apr 18 16:53  admin*
-rwxrwxrwx 1 poh poh 18556 Apr 18 16:39  data.pcap*
-rwxrwxrwx 1 poh poh    28 Apr 18 16:53  login*
-rwxrwxrwx 1 poh poh   219 Apr 18 16:53 'login(2)'*
-rwxrwxrwx 1 poh poh    47 Apr 18 16:53 'login(4)'*
-rwxrwxrwx 1 poh poh  1359 Apr 18 16:53 'login(6)'*
-rwxrwxrwx 1 poh poh   209 Apr 18 16:53  logout*

poh@pohSurface:/mnt/d/pradagy/projects/ctf/pico2018/admin panel$ cat login
user=jimmy&password=p4ssw0rd
poh@pohSurface:/mnt/d/pradagy/projects/ctf/pico2018/admin panel$ cat 'login(2)'
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<title>Redirecting...</title>
<h1>Redirecting...</h1>
<p>You should be redirected automatically to target URL: <a href="/admin">/admin</a>.  If not click the link.
poh@pohSurface:/mnt/d/pradagy/projects/ctf/pico2018/admin panel$ cat 'login(4)'
user=admin&password=picoCTF{n0ts3cur3_df598569}
```

