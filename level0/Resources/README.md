I started to find a file with user name "flag00" in the root with this command:
```
level00@SnowCrash:~$ find / -user 'flag00' 2>/dev/null
/usr/sbin/john
/rofs/usr/sbin/john
level00@SnowCrash:~$
```
I took the contents of the found file and decrypted it using Caesar encryption on the site:
[] https://planetcalc.ru/
```asm
level00@SnowCrash:~$ cat /usr/sbin/john
cdiiddwpgswtgt
level00@SnowCrash:~$ 
```
After decrypting this cipher
cdiiddwpgswtgt
I found only one option with possible code:
![](//Pass_from_Ceaser_Decr.png/150*100)
nottoohardhere
```asm
flag00@SnowCrash:~$ su flag00
Password: 
Don't forget to launch getflag !
flag00@SnowCrash:~$ 
```
Calling <getflag> give us requared pass to level01



