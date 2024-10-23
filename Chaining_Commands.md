## Chaining with semicolon:
when you hit Enter, your shell executes your typed command and, after that command terminates, give you the prompt to input another command. The semicolon is analogous, 
just without the prompt and with you entering both commands before anything is executed.
```bash
Connected!
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{MhykHi6sLTZ8eKSMftxLt8O_anV.dVTN4QDL0YjM0czW}
```
This challenge asked to chain commands in order to get the flag.

## Your first shell script:
We can create a shell script called ```pwn.sh (by convention, shell scripts are frequently named with a sh suffix)```. You need to use ```bash``` command to run the script file like for
ex: ```bash pwn.sh```.
```bash
Connected!
hacker@chaining~your-first-shell-script:~$ touch x.sh
hacker@chaining~your-first-shell-script:~$ nano x.sh
hacker@chaining~your-first-shell-script:~$ cat x.sh
/challenge/pwn

/challenge/college
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{8dC2TlWKMeTn62vYDVCk_Ru_6jr.dFzN4QDL0YjM0czW}
```
This challenge asked to write the previous level command in a bash script so i first created ```x.sh using touch``` and then with ```nano``` command i edited the file and saved it and th
then with ```bash``` command i run the file to get the flag.

## Redirecting script output:
In this i learned how to send the output of several programs to one command .
 ```>``` for stdout, ```2>``` for stderr, ```<``` for stdin, ```>>``` and ```2>>``` for append-mode redirection, ```>&``` for redirecting to other file descriptors, and 
 ```|``` for piping to another command.
 ```bash
hacker@chaining~redirecting-script-output:~$ touch x.sh
hacker@chaining~redirecting-script-output:~$ nano x.sh
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{EV4O9kkeFalGr2fYpN0F6CBCqbd.dhTM5QDL0YjM0czW}
```
Doing the same commands prev i used piping to tranfer the output to another file.

## Executable Shell Script:
```bash
Connected!
hacker@chaining~executable-shell-scripts:~$ touch a.sh
hacker@chaining~executable-shell-scripts:~$ cat a.sh
/challenge/solve
hacker@chaining~executable-shell-scripts:~$ ls -l a.sh
-rwxr--r-- 1 hacker hacker 17 Oct 23 05:38 a.sh
hacker@chaining~executable-shell-scripts:~$ ./a.sh
Congratulations on your shell script execution! Your flag:
pwn.college{omm1z5KJEaM4exOq5bs5j1yHNXL.dRzNyUDL0YjM0czW}
```
i created the file and then entered the command and after i checked the permission and use ```chmod``` to change the permission to enable execute and now without the 
help of ```bash``` i can run it.

