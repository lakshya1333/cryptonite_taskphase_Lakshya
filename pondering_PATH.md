## The PATH Variable
 There is a special shell variable, called ```PATH```, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands . 
 Without a PATH, bash cannot find the ls command . 
 ```bash
hacker@path~the-path-variable:~$ PATH=""
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{QruyWpP1_73wLx02r95hu6ZkRkK.dZzNwUDL0YjM0czW}
```
This challenge asked to remove ```rm``` command from the ```PATH``` to get the flag.

## Setting PATH
By adding directories to or replacing directories in this list, you can expose these programs to be launched using their bare name.
```bash
hacker@path~setting-path:~$ PATH=/challenge/more_commands/
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{EAW1Ob3XVU5_EWW12qmSMGevz_g.dVzNyUDL0YjM0czW}
```

## Adding commands
```bash
hacker@path~adding-commands:~$ mkdir x
hacker@path~adding-commands:~$ cd x
hacker@path~adding-commands:~/x$ touch win
hacker@path~adding-commands:~/x$ nano win
hacker@path~adding-commands:~/x$ cat win
cat /flag
hacker@path~adding-commands:~/x$ echo $PATH
/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~adding-commands:~/x$ ls /usr/bin
hacker@path~adding-commands:~/x$ PATH="/usr/bin:~/x"
hacker@path~adding-commands:~/x$ /challenge/run
Invoking 'win'....
/challenge/run: line 4: /home/hacker/x/win: Permission denied
It looks like that did not work... Did you set PATH correctly?
hacker@path~adding-commands:~/x$ chmod a+x win
hacker@path~adding-commands:~/x$ /challenge/run
Invoking 'win'....
pwn.college{4Lz_B-Z6h0yBhnKteH_8hyIPUqt.dZzNyUDL0YjM0czW}
```
In this challenge, win does not exist. We need to make a shell script called ```win```, add its location to the ```PATH```, and use /challenge/run to find it. 
But because of this, the system won't be able to find commands like cat. Thus we need to use some other method get the flag.
We first create a directory called x. Then inside it, we create a win script inside which we add cat /flag, and then to find which folder is cat in, we use echo $PATH.

##Hijacking commands:
  In this i need to change rm command work so i decided to create a new dir where i overrided the rm command with cat command so now when my program will search for rm command it
  will display the flag. 
  ```bash
Connected!
hacker@path~hijacking-commands:~$ mkdir hello
mkdir: cannot create directory ‘hello’: File exists
hacker@path~hijacking-commands:~$ mkdir fake
hacker@path~hijacking-commands:~$ cd fake
hacker@path~hijacking-commands:~/fake$ echo "/usr/bin/cat /flag" > rm
hacker@path~hijacking-commands:~/fake$ chmod a+rwx rm
hacker@path~hijacking-commands:~/fake$ PATH="~/fake"
hacker@path~hijacking-commands:~/fake$ /challenge/run
Trying to remove /flag...
pwn.college{ALiKPWtFFY8jcUXz-Fk4w6sPL8G.ddzNyUDL0YjM0czW}
```

