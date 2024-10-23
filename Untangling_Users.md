The full list of users on a Linux system is specified in the ```/etc/passwd file```.
Each line contains, separated by :s, the username, an x as a placeholder for where the password used to be
, the numerical user ID, the numerical default group ID, long-form user details, the home directory, and the default shell.
.The nobody user is used to ensure that, e.g., a program runs without any special privileges . 


## Becoming root with su:
```su (the switch user command)``` it runs as root.
```bash
Connected!
hacker@users~becoming-root-with-su:~$ su
Password:
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{ALkLc3JblVDr7TK-jKuvmf8faID.dVTN0UDL0YjM0czW}
```
This challenge gave the password to become root user to get the flag so i used ```su``` command and then entered the pass to become root user and then i did cat /flag to get it.

## Other users with su:
With no arguments, su will start a root shell (after authenticating with root's password). However, you can also give a username as an argument to switch to that user instead of 
root.
```bash
hacker@users~other-users-with-su:~$ su zardus
Password:
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{km7cCqz1PRPZ_joUsJ46rammH_5.dZTN0UDL0YjM0czW}
```
This challenge asked us to switch to zardus user using su and it gave password also after switching i ran the file to get the flag.


## Cracking passwords:
When you enter a password for su, it compares it against the stored password for that user. These passwords used to be stored in ```/etc/passwd```, but because ```/etc/passwd```
is a ```globally-readable```  file, this is not good for passwords, these were moved to ```/etc/shadow```.
A value of * or ! functionally means that password login for the account is disabled, a blank field means that there is no password.
When you input a password into su, it one-way-encrypts (hashes) it and compares the result against the stored value. If the result matches, su grants you access to the user.
If a hacker gets their hands on a leaked ```/etc/shadow```, they can start cracking passwords. The cracking can be done via the famous ```John the Ripper```.
```bash
john is used like this
hacker@dojo:~$ john ./my-leaked-shadow-file
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Will run 32 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
password1337      (zardus)
1g 0:00:00:22 3/3 0.04528g/s 10509p/s 10509c/s 10509C/s lykys..lank
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```
The challenge:

```bash
hacker@users~cracking-passwords:~$ cat /challenge/shadow-leak
root:*:19873:0:99999:7:::
daemon:*:19873:0:99999:7:::
bin:*:19873:0:99999:7:::
sys:*:19873:0:99999:7:::
sync:*:19873:0:99999:7:::
games:*:19873:0:99999:7:::
man:*:19873:0:99999:7:::
lp:*:19873:0:99999:7:::
mail:*:19873:0:99999:7:::
news:*:19873:0:99999:7:::
uucp:*:19873:0:99999:7:::
proxy:*:19873:0:99999:7:::
www-data:*:19873:0:99999:7:::
backup:*:19873:0:99999:7:::
list:*:19873:0:99999:7:::
irc:*:19873:0:99999:7:::
gnats:*:19873:0:99999:7:::
nobody:*:19873:0:99999:7:::
_apt:*:19873:0:99999:7:::
hacker::20000:0:99999:7:::
zardus:$6$Ch9Q7n4RRAmI5on1$0Yyf.p78wv9O6AVAB5TXqG761Yt1wkPrKCmaWFAM9yPlhagtomS29l73MNeMNw92/nC0Q5.6sJLGp3vT0.L.Z1:20019:0:99999:7:::
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Created directory: /home/hacker/.john
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:20 0% 2/3 0g/s 233.3p/s 233.3c/s 233.3C/s rockie..surfing
aardvark         (zardus)
1g 0:00:00:24 100% 2/3 0.04133g/s 240.7p/s 240.7c/s 240.7C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@users~cracking-passwords:~$ su zardus
Password:
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{8-3yGsxZoOVSy5wpt-Qf3FQdoMO.ddTN0UDL0YjM0czW}
```
In this challenge i was given a leak file of shadow i first saw the content to see the pass of zardus then i found that it was encoded so with the help of ```john``` command i decrypted
it and got the pass and with ```su``` command i entered as zardus to get the password.

## Using sudo:
Unlike su, which defaults to launching a shell as a specified user, sudo defaults to running a command as root.
```bash
Connected!
hacker@users~using-sudo:~$ cat /flag
cat: /flag: Permission denied
hacker@users~using-sudo:~$ sudo cat /flag
pwn.college{4SrNFG0v5R_sJve47JIr1LwNJCs.dhTN0UDL0YjM0czW}
```
