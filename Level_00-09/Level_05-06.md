## 🎯 Level 5 -> Level 6
**Objective:** The password is in a file somewhere under the inhere directory and has all of the following properties: human-readable, 1033 bytes in size, not executable.

**Concepts Required:** Finding files based on specific properties.

**Solution:** the level wants us to find a file that have these properties 
*1- human readable*

*2-1033 bytes in size*

*3- not executable*

so we should use `find` command that have a lot of options , we should find the appropriate options from the man page and we'll use these options 

*1- the dot ( . ) for tell the tool to look the current directory [inhere]*

*2- -type to tell the tool to look just for the type that we need [f is suppose to be file]*

*3- -size to tell the tool to look for the size that we need [c is suppose to be bytes]*

*4- -executable to tell the tool to look for the executable files [! suppose to be not executable]*


the final command : `find . -type f -size 1033c ! -executable`

```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit5 bandit0@bandit.labs.overthewire.org -p 2220

bandit5@bandit:~$ ls 
inhere

bandit5@bandit:~$ cd inhere/

bandit5@bandit:~/inhere$ ls -la
total 88
drwxr-x--- 22 root bandit5 4096 Jun 24 14:59 .
drwxr-xr-x  3 root root    4096 Jun 24 14:59 ..
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere00
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere01
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere02
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere03
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere04
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere05
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere06
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere07
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere08
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere09
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere10
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere11
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere12
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere13
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere14
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere15
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere16
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere17
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere18
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere19

bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable
./maybehere07/.file2

bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
