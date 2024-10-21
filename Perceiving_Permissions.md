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
