🎯 Level 2 -> Level 3
Objective: The password for the next level is stored in a file called --spaces in this filename-- located in the home directory.

Concepts Required: Escaping spaces in filenames or using quotes.

Solution: you can use write the full path and use the button TAP to complete the right path because there are spaces and the file name , so the file would take these spaces as another file name 
```bash
ssh -l bandit2 bandit0@bandit.labs.overthewire.org -p 2220


bandit2@bandit:~$ ls -lah 
total 24K
-rw-r-----   1 bandit3 bandit2   33 Jun 24 14:59 --spaces in this filename--
drwxr-xr-x   2 root    root    4.0K Jun 24 14:59 .
drwxr-xr-x 150 root    root    4.0K Jun 24 15:02 ..
-rw-r--r--   1 root    root     220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root    root    3.8K Jun 24 14:50 .bashrc
-rw-r--r--   1 root    root     807 Feb 13 12:16 .profile

bandit2@bandit:~$ cat ./--spaces\ in\ this\ filename-- 
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```
