# OverTheWire: Bandit Writeups

Welcome to my writeups for the [OverTheWire Bandit wargame](https://overthewire.org/wargames/bandit/). 

Bandit is designed for absolute beginners to learn the basics of the Linux command line and security concepts. In this repository, I document my journey through the levels, explaining the tools, concepts, and commands used to solve each challenge.

## ⚠️ Disclaimer
OverTheWire requests that players do not publish the passwords to the levels. In the spirit of the game, my writeups will guide you through the exact commands and logic needed to find the password yourself, but the actual passwords are redacted.

## Table of Contents

### Levels 0 - 9
* [Level 0 -> Level 1](Level_00-09/Level_00-01.md)
* [Level 1 -> Level 2](./Level_00-09/Level_01-02.md)
...

### Levels 10 - 19
* [Level 10 -> Level 11](./Level_10-19/Level_10-11.md)
...
>sfgr
## Level 0 -> 1
the login command:
`ssh -l bandit0 bandit@bandit.labs.overthewire.org -p 2220`
you can use the above command to login to the game using `ssh` 
and you should find a readme file when you do `ls` command 
to read that file use `cat` command and it should be containing the password for the next level 

```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit0 bandit@bandit.labs.overthewire.org -p 2220

bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme 
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: XXXXXXXXXXXXXXXXXXXXXXXX

```
