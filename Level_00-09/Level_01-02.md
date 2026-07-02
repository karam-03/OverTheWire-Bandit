## 🎯 Level 1 -> Level 2
**Objective:** The password for the next level is stored in a file named `-` located in the home directory.

**Concepts Required:** Reading files that start with a dash (which terminal commands usually interpret as a flag).
**Commands Used:** `cat`

**Solution:**
To read a file named `-`, you must specify the current directory path `./` so the `cat` command doesn't confuse the filename with an argument.
```bash
┌──(karam03 ♛ HACKER)-[~/Desktop/OverTheWire-Bandit]
└─$ ssh -l bandit1 bandit0@bandit.labs.overthewire.org -p 2220

bandit1@bandit:~$ cat ./-
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```
