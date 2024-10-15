# Comprehending Commands
## cat: not the pet: <br>
    **cat** command is most often used for reading out files.cat will concatenate (hence the name) multiple files if provided multiple arguments. <br>
    Flag = pwn.college{Mms_Hne2ThTiEJeUc_ykx2GxEvb.dFzN1QDL0YjM0czW} <br>
## catting absolute path: <br>
    Flag = pwn.college{gPpqBpiIKPXBhNmD-ZOA5qN0RWB.dlTM5QDL0YjM0czW} <br>
## more catting: <br>
    Flag = pwn.college{opWYVtD8A7aLrBnRV_FmrSmFBC7.dBjM5QDL0YjM0czW} <br>
## grepping: <br>
    **grep** command is used to search for the contents we need. For ex: grep SEARCH_STRING /path/to/file Invoked like this, grep will search the file for lines of text 
     containing SEARCH_STRING and print them to the console. <br>
     Flag = pwn.college{YJIxPxTU7EazzzW8S5I6fS4TaGI.ddTM4QDL0YjM0czW} ued command  grep pwn /challenge/data.txt <br>
## listing files: <br>
    **ls** will list files in all the directories provided to it as arguments.<br> 
    needed to execute the script <br>
    Flag = pwn.college{825dQIAhmXaFZMgoZL571extWir.dhjM4QDL0YjM0czW}
## touching files <br>
    You can create a new, blank file by touching it with the touch command. <br>
    Flag = pwn.college{4FG2vt1ioHQhyaEBVk2H9W-_sTg.dBzM4QDL0YjM0czW} <br>
## removing files <br>
    In Linux, you remove files with the rm command. <br>
    Flag = pwn.college{cKufd9U4Zk3AWxbWZLWxY8xSkQl.dZTOwUDL0YjM0czW}
## hidden files: <br>
    Linux has a convention where files that start with a . don't show up by default in ls and in a few other contexts.  To view them with ls, you need to invoke ls 
    with the -a flag <br>
    Flag = pwn.college{00Y6ACQqoRjJQRE7Jjh5mKzGPpX.dBTN4QDL0YjM0czW} <br>
## An Epic Filesystem Quest: <br>
    For this i took help from google and used Strings as i as unable to access directly as it was self destructing.  If the file contains readable text, you can 
    try using strings instead of cat.<br>
    for one part used **od** command as strings was not working The od command allows you to read a file's contents byte by byte, potentially avoiding traps that 
    are triggered by reading the whole file at once <br>
    Flag = pwn.college{kE6QLhWPSr7UehiQXV1QY5Y0318.dljM4QDL0YjM0czW} <br>
## making directories: <br>
    You make directories using the mkdir command. <br>
    Flag = pwn.college{k7XyoHTcFTtmCmbeAjsRtPeTW3m.dFzM4QDL0YjM0czW}
## Finding Files: <br
    **find** command is used to find the files.The **find** command takes optional arguments describing the search criteria and the search location. If you don't 
     specify a search criteria, find matches every file. If you don't specify a search location, find uses the current working directory (.). <br>
     Flag = pwn.college{sP3k9kAgUX1Yx5uzB1rlirjEsTL.dJzM4QDL0YjM0czW} the flag was in /usr/local/share/afl/testcases/archives/common/gzip/flag. <br>
## Linking Files: <br>
     Links come in two flavors: hard and soft (also known as symbolic) links.<br>
     Hard = A hard link is when you address your appartment using multiple addresses that all lead directly to the same place (e.g., Apt 2 vs Unit 2). <br>
     Soft = A soft link is when you move appartments and have the postal service automatically forward your mail from your old place to your new place. <br>
     Symbolic links are created with the ln command with the -s argument <br>
     Flag = pwn.college{E7Gj5hGfSoRR0Z8V63K_psZ9SnZ.dlTM1UDL0YjM0czW} i removed the not-the flag file and then use ln -s command to make the catflaf file read the 
     file content. <br>
    
     
    


    

