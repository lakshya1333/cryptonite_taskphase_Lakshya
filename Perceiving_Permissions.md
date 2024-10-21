 You can check out a permissions of a file or directory using ```ls -l```. The first character of each line represents the ```file type``` ```d``` indicates that it's a directory and 
 ```-``` represents that it's a normal file . The next nine characters are the actual access permissions of the file or directory, split into 3 characters denoting the permissions that
 - the user who owns the file (termed the "owner") has to the file, 3 characters denoting the permissions that the group that owns the file (termed the "group") has to the file, and
 -  3 characters denoting the permissions that all other access (e.g., by other users and other groups) has to the file.

 ## Changing File Ownership:
 ```root``` is the administrative acc. 
 To change the ownership of a file use ```chown (change owner) command``` ```chown [username] [file]```.
 ```bash
hacker@permissions~changing-file-ownership:~$ chown hacker /flag
hacker@permissions~changing-file-ownership:~$ cat /flag
pwn.college{0t1Ch_Ld5J7PHXIpE7iiwBhPv6l.dFTM2QDL0YjM0czW}
```
in this challenge i was given power to use ```chown``` command which usually always lie with root user.

## Groups and Files:
A group can have multiple users in it, and a user can be a member of multiple groups. You can check what groups you are part of with the ```id``` command.
group ownership can be changed with the ```chgrp (change group) command```.

```bash
hacker@permissions~groups-and-files:~$ ls -l /flag
-r--r----- 1 root root 58 Oct 21 18:38 /flag
hacker@permissions~groups-and-files:~$ chgrp hacker /flag
hacker@permissions~groups-and-files:~$ ls -l /flag
-r--r----- 1 root hacker 58 Oct 21 18:38 /flag
hacker@permissions~groups-and-files:~$ /flag
ssh-entrypoint: /flag: Permission denied
hacker@permissions~groups-and-files:~$ cat /flag
pwn.college{UrvR-z0fnRnJl66-E7HTnLbQz7U.dFzNyUDL0YjM0czW}
```
First i decided to see the file permission of /flag using ```ls -l``` command which told me that the file can only be access by root user so i used ```chgrp``` command to change the user from root to hacker so that i can access the flag .

## Fun with Group Names:
Not always the group name is same as user it can be different also.
```bash
hacker@permissions~fun-with-groups-names:~$ id
uid=1000(hacker) gid=1000(grp5805) groups=1000(grp5805)
hacker@permissions~fun-with-groups-names:~$ chgrp grp5805 /flag
hacker@permissions~fun-with-groups-names:~$ cat /flag
pwn.college{c7GGosJt5V_Q32aW84GQ2bL98hz.dJzNyUDL0YjM0czW}
```
## Changing Permissions:
r - user/group/other can read the file (or list the directory)
w - user/group/other can modify the files (or create/delete files in the directory)
x - user/group/other can execute the file as a program (or can enter the directory, e.g., using `cd`)
Like ownership we can change file permission also using ```chmod (change mode) command``` we can use like chmod [OPTIONS] MODE FILE .
 chmod allows you to tweak permissions with the mode format of ```WHO+/-WHAT```, where ```WHO``` is user/group/other and ```WHAT``` is read/write/execute.
 ```bash
hacker@permissions~changing-permissions:~$ ls -l /flag
-r-------- 1 root root 58 Oct 21 19:02 /flag
hacker@permissions~changing-permissions:~$ chmod a+r /flag
hacker@permissions~changing-permissions:~$ cat /flag
pwn.college{YGTC203C6GV8i7SpOl2OzDQteEK.dNzNyUDL0YjM0czW}
```
This is how i got the flag.

## Executable Files: 
```bash
hacker@permissions~executable-files:~$ ls -l /challenge/run
-r--r--r-- 1 hacker hacker 32 Jul  4 06:37 /challenge/run
hacker@permissions~executable-files:~$ chmod a+x /challenge/run
hacker@permissions~executable-files:~$ ls -l /challenge/run
-r-xr-xr-x 1 hacker hacker 32 Jul  4 06:37 /challenge/run
^C
hacker@permissions~executable-files:~$ /challenge/run
Successful execution! Here is your flag:
pwn.college{AyAMWhq-PldMmLRWLWyd2tP88qH.dJTM2QDL0YjM0czW}
```
I was asked to change the permission to allow execution also after doing this i got the flag.

## Permission Tweaking Practice:
Till challenge asked to play 8 rounds of changinf permistion and if any round fails game will restart . i started with /challenge/run.
```bash
hacker@permissions~permission-tweaking-practice:~$ /challenge/run
Round 0 (of 8)!

Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": ---r--r--
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
```u -rw``` was required after comparing.
```bash
hacker@permissions~permission-tweaking-practice:~$ chmod u-rw /challenge/pwn
You set the correct permissions!
Round 1 (of 8)!

Current permissions of "/challenge/pwn": ---r--r--
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": --xr-xr--
- the user doesn't have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```

after comparing ```u+x,g+x``` was required.

```bash
hacker@permissions~permission-tweaking-practice:~$ chmod u+x,g+x /challenge/pwn
You set the correct permissions!
Round 2 (of 8)!

Current permissions of "/challenge/pwn": --xr-xr--
- the user doesn't have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": --xr-xr-x
- the user doesn't have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
```
After comparing ```o+x``` was required.

```bash
hacker@permissions~permission-tweaking-practice:~$ chmod o+x /challenge/pwn
You set the correct permissions!
Round 3 (of 8)!

Current permissions of "/challenge/pwn": --xr-xr-x
- the user doesn't have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": --xr--r--
- the user doesn't have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```

After comparing ```g-x,o-x``` was required.

```bash
hacker@permissions~permission-tweaking-practice:~$ chmod g-x,o-x /challenge/pwn
You set the correct permissions!
Round 4 (of 8)!

Current permissions of "/challenge/pwn": --xr--r--
- the user doesn't have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r-xr--r--
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```

After comparing ```u+r``` was req

```bash
hacker@permissions~permission-tweaking-practice:~$ chmod u+r /challenge/pwn
You set the correct permissions!
Round 5 (of 8)!

Current permissions of "/challenge/pwn": r-xr--r--
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r-xr-xr-x
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
```

After comparing ```g+x,o+x``` was req.

```bash
hacker@permissions~permission-tweaking-practice:~$ chmod g+x,o+x /challenge/pwn
You set the correct permissions!
Round 6 (of 8)!

Current permissions of "/challenge/pwn": r-xr-xr-x
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```

After comparing ```u-x,g-x,o-x``` was req

```bash
hacker@permissions~permission-tweaking-practice:~$ chmod u-x,g-x,o-x /challenge/pwn
You set the correct permissions!
Round 7 (of 8)!

Current permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r--r-----
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```

After comparing ```o-r``` was req finally to get the flag

```bash
hacker@permissions~permission-tweaking-practice:~$ chmod o-r /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod u+r /flag
hacker@permissions~permission-tweaking-practice:~$ cat /flag
pwn.college{8ydYY9ZWRXylEzErFwhoSgNl388.dBTM2QDL0YjM0czW}
```

##Permission Setting:





