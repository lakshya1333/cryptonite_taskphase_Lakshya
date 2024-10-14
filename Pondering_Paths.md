# This module taught the basics of Linux file paths.
## The Root: <br>
    root directory (/) <br>
    This style of path, one that starts with the root directory, is referred to as an "absolute path" for ex: /pwn. <br> 
    Flag = pwn.college{McqxmSNxHpza3Ks5onDhjzBrfnG.dhzN5QDL0YjM0czW} <br>
## Program and Absolute Paths: <br>
    The flag was in /challenge/run which is a absolute path. <br>
    Flag = pwn.college{IVANjfmsWTzYzZWET0YavFEu3vo.dVDN1QDL0YjM0czW} <br>
## Position Thy Self: <br>
    We can navigate around directories by using the cd (change directory) command and passing a path to it as an argument. <br>
    The ~ argument shows the current path that your shell is located at. <br>
    In this challenge initially i was in /home/hacker i need to use cd command to change it to other directory to get the flag . After i run /challenge/run it asked me to go to 
    /proc/67/fd first and then i run cd /challenge/run to get the flag . <br>
    Flag = pwn.college{IeIbgUB4lDYKGIuEfFdvgXxCsRj.dZDN1QDL0YjM0czW} <br>
## Position elsewhere: <br>
    It was similar to the last one only first i tried to go directly to challenge/run but then it told the path from where i need to go which was /sys/kernel so i first changed 
    it into that using cd and then i found the flag . <br>
    Flag = pwn.college{0XUk8i2IllcCbn9MSqw7arBFDgv.ddDN1QDL0YjM0czW} <br>
## Position yet elsewhere: <br>
    I was also same only like the previous ones here i first cd to challenge directly where i did /challenge/run but then i told me to go to /usr/aarch64-linux-gnu/include/gnu 
    and i repeated the same stuff. <br>
    Flag = pwn.college{4mT2DLV-PkV084EIELbWf0RKXcV.dhDN1QDL0YjM0czW} <br>

    
    
    
    

