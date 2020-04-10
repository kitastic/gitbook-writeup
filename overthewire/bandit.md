# Bandit

## Using WeChall Scoreboard to keep track of progress

1. First, go to [WeChall](https://www.wechall.net/) and register for an account.
2. Next, log in and retrieve your WeChall token and username. Your WeChall username is what you registered with, while your WeChall token can be found on the WeChall website under [“Account” -&gt; “WarBoxes”](https://www.wechall.net/warboxes). The token looks something like “EDD76-1FC9F-7388B-DC6EB-E3F71-FC4CB”.
3. Next, assuming you are using the correct operating system, edit your ~/.bashrc file and add:

   ```text
   export WECHALLUSER="YourUserName"
   export WECHALLTOKEN="YOUR-WECHALL-TOKEN-HERE"
   ```

   \*If you are using Windows 10 \(WSL\), you can either use the Ubuntu terminal which automatically loads the bashrc file or the file can be found in C:\Users\USERNAME\AppData\Local\Packages\{LINUX\_DISTRIBUTION}\LocalState\rootfs\home\{LINUXUSER}\

  
   For `fish` users, you may run:

   ```text
   set -Ux WECHALLUSER "YourUserName"
   ```

   You may need to logout and login again for these changes to take effect. To test whether the environment variables are registered, type “echo $WECHALLUSER”, which should show that environment variable.

4. Next, edit ~/.ssh/config \(or create it if it doesn’t exist\) and add:

   ```text
   Host *.labs.overthewire.org
     SendEnv WECHALLTOKEN
     SendEnv WECHALLUSER
   ```

   This configures your SSH client to transmit both username and token to your remote session, so it can be used there.

5. Finally, you are able to easily register which levels you have beaten on OverTheWire by logging in through SSH the normal way, and invoking the “wechall” command. This command will use your WeChall username and WeChall token to register the level you have beaten with WeChall.  `WECHALLUSER="tokumeipoh" WECHALLTOKEN="129CF-40592-FCDCF-67470-6F4EA-D5DB1" wechall`

### Level 0

> The goal of this level is for you to log into the game using SSH. The host to which you need to connect is **bandit.labs.overthewire.org**, on port 2220. The username is **bandit0** and the password is **bandit0**. Once logged in, go to the [Level 1](https://overthewire.org/wargames/bandit/bandit1.html) page to find out how to beat Level 1.

{%hint style="info"%}
If you get an ssh error

`Bad owner or permissions on /home/{user}/.ssh/config`

You need to set rw permission only for the user

```text
chmod 600 ~/.ssh/config
// or
chown $USER ~/.ssh/config
```
{% endhint %}

> The password for the next level is stored in a file called **readme** located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH \(on port 2220\) to log into that level and continue the game.

Use cat command to read the file and get the password. Then use that password to login to the same server with incrementing bandit number as the username. E.g.   
_`sudo bandit1@bandit.labs.overthewire.org -p 2220`_

### _Level 1_

> The password for the next level is stored in a file called **-** located in the home directory
>
> ### Commands you may need to solve this level <a id="commands-you-may-need-to-solve-this-level"></a>
>
> ls, cd, cat, file, du, find
>
> ### Helpful Reading Material <a id="helpful-reading-material"></a>
>
> * [Google Search for “dashed filename”](https://www.google.com/search?q=dashed+filename)
> * [Advanced Bash-scripting Guide - Chapter 3 - Special Characters](http://tldp.org/LDP/abs/html/special-chars.html)

In order for cat to consider the dash a filename instead of STDIN/STDOUT, you have to specify path such as \(if in same directory\)

```bash
cat ./-
```

### Level 2

> The password for the next level is stored in a file called **spaces in this filename** located in the home directory
>
> ### Commands you may need to solve this level <a id="commands-you-may-need-to-solve-this-level"></a>
>
> ls, cd, cat, file, du, find
>
> ### Helpful Reading Material <a id="helpful-reading-material"></a>
>
> * [Google Search for “spaces in filename”](https://www.google.com/search?q=spaces+in+filename)

Either access the whole filename inside double quotes or escape each space with a back slash

```bash
cat "spaces in this filename"
// or
cat spaces\ in\ this\ filename
```

### Level 3

> The password for the next level is stored in a hidden file in the **inhere** directory.
>
> ### Commands you may need to solve this level <a id="commands-you-may-need-to-solve-this-level"></a>
>
> ls, cd, cat, file, du, find

Hidden files usually has a period in front of their names. To list hidden files, pass the option -al. Once you know the name of the hidden file, you can cat the filename.

```bash
ls -al            //to list all files including hidden ones
cat ./.hidden     // file called ".hidden" was found
```

### Level 4

> The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the “reset” command.
>
> ### Commands you may need to solve this level <a id="commands-you-may-need-to-solve-this-level"></a>
>
> ls, cd, cat, file, du, find



