I started to find a file with user name "flag00" in the root with this command:
```shell
level00@SnowCrash:~$ find / -user 'flag00' 2>/dev/null
/usr/sbin/john
/rofs/usr/sbin/john
level00@SnowCrash:~$
```


I took the contents of the found file and decrypted it using Caesar encryption on the site:
 https://planetcalc.ru/
```shell
level00@SnowCrash:~$ cat /usr/sbin/john
cdiiddwpgswtgt
level00@SnowCrash:~$ 
```
After decrypting this cipher
cdiiddwpgswtgt
I found only one option with possible code:
![](Images/test.jpg/150*100 "Decrypted keyword")
nottoohardhere
```shell
flag00@SnowCrash:~$ su flag00
Password: 
Don't forget to launch getflag !
flag00@SnowCrash:~$ 
```
Calling "getflag" give us requared pass to level01



