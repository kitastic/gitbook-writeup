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



