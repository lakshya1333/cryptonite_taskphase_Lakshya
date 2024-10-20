## Matching with *:
The first glob we'll learn is *. When it encounters a * character in any argument, the shell will treat it as "wildcard" and try to replace that argument with any 
files that match the pattern.
The * matches any part of the filename except for / or a leading . character. 
```bash
Connected!
This challenge resets your working directory to /home/hacker unless you change
directory properly...
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{86tW3oJl0EEcSNYfpOXhW2weTtU.dFjM4QDL0YjM0czW}
```
i used cd /ch* which resulted in /challenge and this is how i got the flag.

## Matching with ?:

