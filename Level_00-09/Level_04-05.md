## 🎯 Level 4 -> Level 5
**Objective:** The password is in the only human-readable file in the inhere directory.

**Concepts Required:** Determining file types.

**Solution:** you need to check the file types before reading them because you need to know the human readable file , the human readable files actally can be written an ASCII code *ASCII code is the encoding method to translate the hex digits into anything that can be written in a keyboard* so use `cat` on `-file07` and the key will be found inside it 

```bash
┌──(karam03 ♛ HACKER)-[~/Desktop/OverTheWire-Bandit]
└─$ ssh -l bandit4 bandit0@bandit.labs.overthewire.org -p 2220

bandit4@bandit:~$ ls -lah
total 24K
drwxr-xr-x   3 root root 4.0K Jun 24 14:59 .
drwxr-xr-x 150 root root 4.0K Jun 24 15:02 ..
-rw-r--r--   1 root root  220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root root 3.8K Jun 24 14:50 .bashrc
-rw-r--r--   1 root root  807 Feb 13 12:16 .profile
drwxr-xr-x   2 root root 4.0K Jun 24 14:59 inhere
bandit4@bandit:~$ cd inhere/

bandit4@bandit:~/inhere$ ls -lah
total 48K
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file00
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file01
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file02
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file03
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file04
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file05
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file06
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file07
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file08
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file09
drwxr-xr-x 2 root    root    4.0K Jun 24 14:59 .
drwxr-xr-x 3 root    root    4.0K Jun 24 14:59 ..

bandit4@bandit:~/inhere$ file ./-file0*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: OpenPGP Public Key
./-file07: ASCII text
./-file08: data
./-file09: Motorola S-Record; binary data in text format

bandit4@bandit:~/inhere$ cat ./-file07
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
