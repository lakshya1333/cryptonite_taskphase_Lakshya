Linux has three channels:
Standard Input is the channel through which the process takes input. For example, your shell uses Standard Input to read the commands that you input.
Standard Output is the channel through which processes output normal data, such as the flag when it is printed to you in previous challenges or the output of utilities such as ls.
Standard Error is the channel through which processes output error details. For example, if you mistype a command, the shell will output, over standard error, that this command does not exist.

These three are also k/as ```stdin, stdout, stderr```


## Redirecting Output:
You can use ```>``` command to redirect the output to a specific file and then use cat to get the output from the file.
```bash
Connected!
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your
flag:
pwn.college{wBplyN0e_NzRr3LfjaU3Y2lTJTz.dRjN1QDL0YjM0czW}
```
In this challenge i just have to save PWN in COLLEGE file and this is how i got the file.

## Redirecting More Output:
```bash
Connected!
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{Eg7soB2N7vpRliZYfQm1lr4pDm1.dVjN1QDL0YjM0czW}
```
 In this instead of a echo command i need to use /challenge/run to transfer its output to a file and then use cat to get the flag.

 ## Appending Output:
 To append in already created file use >> instead of > it will append then not replace.
 ```bash
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do
the first write directly to the file, and the second write, I'll do to stdout
(if it's pointing at the file). If you redirect the output in append mode, the
second write will append to (rather than overwrite) the first write, and you'll
get the whole flag!
hacker@piping~appending-output:~$ cat  /home/hacker/the-flag
 |
\|/ This is the first half:
 v
pwn.college{Ehdah7fh2JiU0Nz6_x9L2RrC1IS.ddDM5QDL0YjM0czW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>)
rather than *append* mode (>>), and so the write of the second half to stdout
overwrote the initial write of the first half directly to the file. Try append
mode!
```
I needed to use >> instead of > to get both parts of the flag.

## Redirecting errors :
A File Descriptor (FD) is a number the describes a communication channel in Linux.
FD 0: Standard Input
FD 1: Standard Output
FD 2: Standard Error
a > without a number implies 1>, which redirects FD 1 (Standard Output). Thus, the following two commands are equivalent.
```bash
Connected!
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{ssCip1nxdmHUnHXHYw-PVSxamNc.ddjN1QDL0YjM0czW}
```
The challenge asked me to transfer the output to myflag file and error to instructions.

## Redirecting Input:
Redirecting input is done using ```<``` command.
```bash
Connected!
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run <PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{YKu-V5zT_gRyL9SMWdPfugGKFtK.dBzN1QDL0YjM0czW}
```
In this i need to first write in the file and then i was asked to redirect it.

## Grepping Stored Results:
This challenge has asked to use ```>``` and ```grep``` commands.
```bash
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep pwn /tmp/data.txt
pwn.college{UfLavlQpZYmSiE2kW02M6bZohEJ.dhTM4QDL0YjM0czW}
pwned
pwns
pwn
pwning
```
This is how i got the flag.

## Grepping live output:
We can use pipe ```|``` operator to remove the middlemand like not storing anywhere the file to grep it. It will be connected.
```bash
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwning
pwns
pwned
pwn.college{gMgUeRX4DDcZqsdRdfMLTsgxE67.dlTM4QDL0YjM0czW}
pwn
```
i used to grep to search for the pwn word from the output instead of storing the output somewhere.

## Grepping Errors:
The shell has a >& operator, which redirects a file descriptor to another file descriptor. This means that we can have a two-step process to grep through errors: first, we redirect standard error to standard output (2>& 1) and then pipe the now-combined stderr and stdout as normal (|)!.
```bash
hacker@piping~grepping-errors:~$ /challenge/run 2>&1 | grep 'pwn'
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwning
pwn.college{Q9FvfmTY-EtZL6Shyp8BUllrW0L.dVDM5QDL0YjM0czW}
pwn
pwns
pwned
```
This challenge was cool as i was asked to Redirect standard error (stderr, file descriptor 2) to standard output (stdout, file descriptor 1) . THis cannot be done using ```>``` so i was asked to use ```2>&1``` which redirects stderr (fd 2) to stdout (fd 1). after that i used ```grep``` command to find the flag that starts with pwn.

## Duplicating pipe data with tee:

