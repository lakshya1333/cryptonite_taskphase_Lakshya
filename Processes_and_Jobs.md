## Listing Processes:
We can list running processes using the ```ps``` command. ```ps``` stands for "process snapshot" or "process status". By default, ps just lists the processes running in your terminal.
We can see that each process has a numerical identifier (the Process ID, or PID), which is a number that uniquely identifies every running process in a Linux environment. 
We also see the terminal on which the commands are running (in this case, the designation pts/0), and the total amount of cpu time that the process has eaten up so far.
There are many arguments u can use it with you can use -e to list "every" process and -f for a "full format" output, including arguments. 
These can be combined into a single argument -ef. ```"BSD" Syntax:``` in this syntax, you can use a to list processes for all users, x to list processes that aren't running in a terminal, 
and u for a "user-readable" output. These can be combined into a single argument aux.
These two methods, ```ps -ef and ps aux``` result in slightly different, but cross-recognizable output.
There are many commonalities between ps -ef and ps aux: both display the user (USER column), the PID, the TTY, the start time of the process (STIME/START), the total utilized CPU time (TIME),
and the command (CMD/COMMAND). ps -ef additionally outputs the Parent Process ID (PPID), which is the PID of the process that launched the one in question, while ps aux outputs the percentage of total system CPU and Memory that the process is utilizing.
```bash
Connected!
hacker@processes~listing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 13:02 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /ru
root           7       1  0 13:02 ?        00:00:00 /run/dojo/bin/sleep 6h
root          68       1  0 13:02 ?        00:00:00 /challenge/6387-run-7049
root          72      68  0 13:02 ?        00:00:00 sleep 6h
hacker        73       0  0 13:02 pts/0    00:00:00 /run/dojo/bin/ssh-entrypoint
hacker        90      73  0 13:02 pts/0    00:00:00 ps -ef
hacker@processes~listing-processes:~$ /challenge/6387-run-7049
Yahaha, you found me! Here is your flag:
pwn.college{8Vq12jjjSo2PTFM-eSVlzz7ardG.dhzM4QDL0YjM0czW}
Now I will sleep for a while (so that you could find me with 'ps').
```

## Killing Processes:
You can kill a process using ```kill``` command. kill will terminate a process in a way that gives it a chance to get its affairs in order before ceasing to exist.
You use kill to terminate by passing the process identifier (the PID from ps) as an argument.
```bash
Connected!
hacker@processes~killing-processes:~$ ps -ef | grep dont_run
hacker        73      71  0 13:06 ?        00:00:00 /challenge/dont_run
hacker        93      75  0 13:06 pts/0    00:00:00 grep --color=auto dont_run
hacker@processes~killing-processes:~$ kill 73
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{EvSoPAQMkFQy4AQT0SSqevbyAeh.dJDN4QDL0YjM0czW}
```
i used grep to find dont_run easily and then i used its PID to kill the process in order to get the flag.

## Interrupting Processes:
You can stop a process in b/w using ```ctrl+c```.
```bash
Connected!
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember,
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{81-J6rm8zhqRxdEFXLZxBvdHTja.dNDN4QDL0YjM0czW}
```
## Suspending Processes:
Instead of stopping it we can suspend it using ```ctrl+z``` command.
```bash
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          82      65  0 13:11 pts/0    00:00:00 bash /challenge/run
root          84      82  0 13:11 pts/0    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can
background me with Ctrl-Z or, if you're not ready to do that for whatever
reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          82      65  0 13:11 pts/0    00:00:00 bash /challenge/run
root          89      65  0 13:12 pts/0    00:00:00 bash /challenge/run
root          91      89  0 13:12 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{UBrLoSyIJLFJaDGH9BipydJBR7Y.dVDN4QDL0YjM0czW}
```

## Resuming processes:
To resume a suspended program use ```fg``` command, a builtin that takes the suspended process, resumes it, and puts it back in the foreground of your terminal.
```bash
Connected!
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg /challenge/run
/challenge/run
I'm back! Here's your flag:
pwn.college{4tZZnSf4mMPsSE9oNm0iqphSrgP.dZDN4QDL0YjM0czW}
Don't forget to press Enter to quit me!

Goodbye!
```

## Backgrounding Processes:
if u dont want to resume program in front and want it to run in background so that ypu can enter more commands in the terminal use ```bg``` command.
```bash
Connected!
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S+   bash /challenge/run
root          84 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the
background, and then launch a new version of me! You can background me with
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ bg /challenge/run
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out.
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S    bash /challenge/run
root          92 S    sleep 6h
root          93 S+   bash /challenge/run
root          95 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{EpabG99-B3uyKODd8zKZXQa-Uhg.ddDN4QDL0YjM0czW}
```
I first run the program and then usiong bg command i put into background to run the another copy of same program to get the flag.

## Foregrounding Process:
```bash
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the
background, and *then* foreground it without re-suspending it! You can
background me with Ctrl-Z (and resume me in the background with 'bg') or, if
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~foregrounding-processes:~$ bg /challenge/run
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out. After that, resume me into the foreground with 'fg';
I'll wait.
hacker@processes~foregrounding-processes:~$ fg /challenge/run
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!
pwn.college{A-0AJcjB5zSMbt-ESBKSTZ72V1X.dhDN4QDL0YjM0czW}
```

I first run the file to see what is the output then after it told me what to do . I suspended it first and then run it in the 
background and then i run it in forefront using fg command to get the flag after entering ENTER.

## Starting Background Processes:
We dont have to suspend the process always to put it in the background instead we have to do is append a ```&``` to the command.
```bash
hacker@processes~starting-backgrounded-processes:~$ /challenge/run
You've started me in the foreground! You must start me in the background (by
appending '&' to the command) to get the flag!
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 86



Yay, you started me in the background! Because of that, this text will probably
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{MK1jlgTAdMHOfF6Zd3tICfxOYEy.dlDN4QDL0YjM0czW}
[1]+  Done                    /challenge/run
```
I needed to appemnd & to run it in the background to get the flag.

## Process Exit Code:
Every shell command, including every program and every builtin, exits with an ```exit code``` when it finishes running and terminates.We can use it 
to check if the process succeeded in its functionality. We can access the exit code of the most recently-terminated command using the special ? variable (don't forget to 
prepend it with $ to read its value!).
Commands that succeed typically return 0 and commands that fail typically return a non-zero value, most commonly 1 but sometimes an error code that identifies a specific failure mode.
```bash
Connected!
hacker@processes~process-exit-codes:~$ /challenge/get-code
Exiting with an error code!
hacker@processes~process-exit-codes:~$ echo $?
12
hacker@processes~process-exit-codes:~$ /challenge/submit-code 12
CORRECT! Here is your flag:
pwn.college{o-Y0Ap_uCLSURZXvf8MI8gPhXoX.dljN4UDL0YjM0czW}
```




