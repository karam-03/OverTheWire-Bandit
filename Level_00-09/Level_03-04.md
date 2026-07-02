## 🎯 Level 3 -> Level 4
**Objective:** The password is in a hidden file in the inhere directory.

**Concepts Required:** Viewing hidden files.

**Solution:** we should search for the hidden file in the `inhere` direcroty and we found it using `ls -lah` command and the plugin `-a` allows us to see the hidden files inside the directory and we found this file `...Hiding-From-You` so we used `cat` to read it's content  
```bash
┌──(karam03 ♛ HACKER)-[~/Desktop/OverTheWire-Bandit]
└─$ ssh -l bandit3 bandit0@bandit.labs.overthewire.org -p 2220

bandit3@bandit:~$ ls -lah
total 24K
drwxr-xr-x   3 root root 4.0K Jun 24 14:59 .
drwxr-xr-x 150 root root 4.0K Jun 24 15:02 ..
-rw-r--r--   1 root root  220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root root 3.8K Jun 24 14:50 .bashrc
-rw-r--r--   1 root root  807 Feb 13 12:16 .profile
drwxr-xr-x   2 root root 4.0K Jun 24 14:59 inhere

bandit3@bandit:~$ cd inhere/

bandit3@bandit:~/inhere$ ls -lah
total 12K
drwxr-xr-x 2 root    root    4.0K Jun 24 14:59 .
drwxr-xr-x 3 root    root    4.0K Jun 24 14:59 ..
-rw-r----- 1 bandit4 bandit3   33 Jun 24 14:59 ...Hiding-From-You

bandit3@bandit:~/inhere$ cat ...Hiding-From-You 
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```
