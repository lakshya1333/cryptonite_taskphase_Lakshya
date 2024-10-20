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
I learnt about ?. When it encounters a ? character in any argument, the shell will treat it as single-character wildcard. This works like *, but only matches one character.
```bash
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{AVTnF8Y4Cjc_4xhaP5RjfxTX_qP.dJjM4QDL0YjM0czW}
```
it asked me to not use c and l while changing directory thats why i used ? which will get me the character.

## Matching with []:
In this I learned about []. The square brackes are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, or n.
```bash
hacker@globbing~matching-with-:~$ cd /
hacker@globbing~matching-with-:/$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$  /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{Q59EuvvVxxpSkUwc8Nmg-lCUsuw.dNjM4QDL0YjM0czW}
```
i used [bash] which will return me the files which has b a s h that is what the q asked.

## Matching path with []:
I learnt that Globbing happens on a path basis, so we can expand entire paths with the globbed arguments.
```bash
Connected!
hacker@globbing~matching-paths-with-:~$ cd ~
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[absh]
You got it! Here is your flag!
pwn.college{Y9xoiiN3rpJxYwfACr_qZbLAFNm.dRjM4QDL0YjM0czW}
```
I first changed to /home/hacker dir and from there i run the command the q asked and got the flag

## Mixing Glob:
```bash
Connected!
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ ls
amazing      delightful   great       jovial    magical     pwning   splendid   victorious  youthful
beautiful    educational  happy       kind      nice        queenly  thrilling  wonderful   zesty
challenging  fantastic    incredible  laughing  optimistic  radiant  uplifting  xenial
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{QjsROMPzbr5EETJ3NGKqY7HOkVu.dVjM4QDL0YjM0czW}
```
In this i was asked to use whatever i learnt till now to list 3 files.

## Exclusionary Globbing:
Sometimes, We want to filter out files in a glob! Luckily, [] helps you do just this. If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed.

```bash
hacker@globbing~exclusionary-globbing:/$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{U5rwCVl7YaSKlwiKpYTahm8FRaP.dZjM4QDL0YjM0czW}
```
There was a problem in starting it was saying it should be small but when i resetted the terminal it was working properly.

