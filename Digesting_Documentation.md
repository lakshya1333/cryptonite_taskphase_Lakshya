## Learning From Documentation:
We need to be sure what type of arguments we are giving.
In this, it has asked to find a flag by using `--giveflag` and proper arguments.
```bash
hacker@man~learning-from-documentation:~$ cd /
hacker@man~learning-from-documentation:/$ challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{k9pu4EGgRPOi3qnPvCDH6_DL8c1.dRjM5QDL0YjM0czW}
```
This is how i got the flag ```pwn.college{k9pu4EGgRPOi3qnPvCDH6_DL8c1.dRjM5QDL0YjM0czW}```.

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
I saw that ```/challenge/challenge --printfile /challenge/DESCRIPTION.md``` was printing the description so i checked out the directory contents and i found that that there is a flag so i used the same command only replacing the words after ```--printfile to /flag /challenge/challenge --printfile /flag``` it gave me the flag .

## Reading Manuals:
`man` is short for manual, and will display (if available) the manual of the command you pass as an argument. You can quit the manula using 'q'.<br>
In this challenge i need to have look on the man page of challenge command and find something unique which will get me the flag. <br>
```bash
hacker@man~reading-manuals:~$ man challenge

CHALLENGE(1)                                      Challenge Commands                                     CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --fxutwl NUM
              print the flag if NUM is 423

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)
hacker@man~reading-manuals:~$
hacker@man~reading-manuals:~$ /challenge/challenge --fxutwl 423
Correct usage! Your flag: pwn.college{4K2f3x3uO0-Stwl7QQtc-PWOToI.dRTM4QDL0YjM0czW}
```
First i saw the manual of challenge command using ```man``` and there i found the the way to get the flag i need to give ```/challenge/challenge --fxutwl 423``` as the command to get the flag ```pwn.college{4K2f3x3uO0-Stwl7QQtc-PWOToI.dRTM4QDL0YjM0czW}```.

## Searching Manuals: 
We can scroll ```man``` pages with the arrow keys (and PgUp/PgDn) and search with ```/```. After searching, you can hit ```n``` to go to the next result and ```N``` to go to the previous result. Instead of /, you can use ```?``` to search backwards.
The manual was very big but i used ```/``` to search for flag which made this level easy where i found the argument needed to give to get the flag which was ```--lswgf This argument will give you the flag!```
```bash
hacker@man~searching-manuals:~$ /challenge/challenge --lswgf
Initializing...
Correct usage! Your flag: pwn.college{QjgL2lGm6IqPH7jY7p1Vj2Gerpy.dVTM4QDL0YjM0czW}
hacker@man~searching-manuals:~$
```
Then by giving the proper command i got the flag ```pwn.college{QjgL2lGm6IqPH7jY7p1Vj2Gerpy.dVTM4QDL0YjM0czW}```.

## Searching for manuals: 

We can read man page using ```man man``` command. I need to used this command to figure out how to search for the hidden manpage that will tell me how to use /challenge/challenge .
After doing man man i found out this  man -k printf command which Search the short descriptions and manual page names for the keyword printf as regular  expression and Print out any matches. Equivalent to apropos printf.
```bash
hacker@man~searching-for-manuals:~$ man -k /challenge/challenge
sdrjovlnbs (1)       - print the flag!
hacker@man~searching-for-manuals:~$ man sdrjovlnbs

CHALLENGE(1)                                      Challenge Commands                                     CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --sdrjov NUM
              print the flag if NUM is 864

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)
hacker@man~searching-for-manuals:~$
hacker@man~searching-for-manuals:~$ sdrjovlnbs --sdrjov 864
ssh-entrypoint: sdrjovlnbs: command not found
hacker@man~searching-for-manuals:~$ /challenge/challenge --sdrjov 864
Correct usage! Your flag: pwn.college{IsR_Hd8rLTIjovE_lRnGbsClcw6.dZTM4QDL0YjM0czW}
```
after using the  ```man -k /challenge/challenge command``` i found the name and then i used ```man``` to see if i need to give any argument after that i used it to get the flag pwn.college{IsR_Hd8rLTIjovE_lRnGbsClcw6.dZTM4QDL0YjM0czW}.

## Helpful Programs: 

What if man is not present for a specific command? No problem we can use --help, but it can often be -h or, in rare cases, -?, help, or other esoteric values like /? (though that latter is more frequently encountered on Windows). <br>
in this challenge i need to use --help to read a program documentation to get the flag.
After reading the documentation using ```/challenge/challenge -h``` i found this: 
```bash
hacker@man~helpful-programs:~$ /challenge/challenge -h
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
```
But when i run ```/challenge/challenge -g GIVE_THE_FLAG``` i came to know that instead of GIVE_THE_FLAG a ```int number``` will come.
```bash
hacker@man~helpful-programs:~$ /challenge/challenge -g GIVE_THE_FLAG
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]
a challenge to make you ask for help: error: argument -g/--give-the-flag: invalid int value: 'GIVE_THE_FLAG'
```
and then i decided to use -p command to see if a number prints and it works.
```bash
hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 401
hacker@man~helpful-programs:~$ /challenge/challenge -g 401
Correct usage! Your flag: pwn.college{Yzjh40vLY-1uyh_J485CaOM4RXl.ddjM4QDL0YjM0czW}
```
This is how i got the flag.

## Help for Builtins:
   



