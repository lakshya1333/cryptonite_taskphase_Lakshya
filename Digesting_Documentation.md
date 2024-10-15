## Learning From Documentation:
We need to be sure what type of arguments we are giving.
In this, it has asked to find a flag by using `--giveflag` and proper arguments.
```bash
hacker@man~learning-from-documentation:~$ cd /
hacker@man~learning-from-documentation:/$ challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{k9pu4EGgRPOi3qnPvCDH6_DL8c1.dRjM5QDL0YjM0czW}
```
This is how i got the flag pwn.college{k9pu4EGgRPOi3qnPvCDH6_DL8c1.dRjM5QDL0YjM0czW}.

## Learning complex usage: 
There are commands that take arguments to their arguments like `find` command.
In this i need to use --printfile argument by proper arguments after it to get the flag.
```bash
hacker@man~learning-complex-usage:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  opt   root  sbin  sys  usr
boot  dev        flag  lib   lib64  media   nix  proc  run   srv   tmp  var
hacker@man~learning-complex-usage:/$ /challenge/challenge --printfile /challenge/DESCRIPTION.md
Correct argument! Here is the /challenge/DESCRIPTION.md file:
While using most commands is straightforward, the usage of some commands can get quite complex.
For example, the arguments to commands like `sed` and `awk`, which we're definitely not getting into right now, are entire programs in an esoteric programming language!
Somewhere on the spectrum between `cd` and `awk` are commands that take arguments to their arguments...

This sounds crazy, but you've already encountered this with the `find` level in [Basic Commands](../commands).
`find` has a `-name` argument, and the `-name` argument itself takes an argument specifying the name to search for.
Many other commands are analogous.

Here is this level's documentation for `/challenge/challenge`:

> Welcome to the documentation for `/challenge/challenge`! This program allows you to print arbitrary files to the terminal, when given the `--printfile` argument. The argument to the `--printfile` argument is the path of the flag to read. For example, `/challenge/challenge --printfile /challenge/DESCRIPTION.md` will print out the description of the level!

Given that documentation, go get the flag!
hacker@man~learning-complex-usage:/$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{8gXTcMbqerct2xdIJf_JyTktU38.dVjM5QDL0YjM0czW}
```
I saw that /challenge/challenge --printfile /challenge/DESCRIPTION.md was printing the description so i checked out the directory contents and i found that that there is a flag so i used the same command only replacing the words after --printfile to /flag /challenge/challenge --printfile /flag it gave me the flag .
