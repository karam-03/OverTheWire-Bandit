# OverTheWire: Bandit — Writeup

Welcome to my writeups for the [OverTheWire Bandit wargame](https://overthewire.org/wargames/bandit/).

Bandit is designed for absolute beginners to learn the basics of the Linux command line and security concepts. In this repository, I document my journey through the levels, explaining the tools, concepts, and commands used to solve each challenge.

**Server:** `bandit.labs.overthewire.org` on port `2220`
**Format:** each section explains the goal of the level, the concept/command you need to learn, and the exact commands used to solve it.

> ⚠️ **Security note:** passwords are intentionally shown as `<PASSWORD>` placeholders in this repo. Never commit real Bandit passwords to a public repo — the whole point of the game is that each password is meant to stay private to whoever solves the level. Replace the placeholder with what you find on your own terminal.

---
## Table of Contents 
#### Linux basics (0–9) 
* [Level 0 → 1](#level-0--1) 
* [Level 1 → 2](#level-1--2) 
* [Level 2 → 3](#level-2--3) 
* [Level 3 → 4](#level-3--4) 
* [Level 4 → 5](#level-4--5) 
* [Level 5 → 6](#level-5--6) 
* [Level 6 → 7](#level-6--7) 
* [Level 7 → 8](#level-7--8) 
* [Level 8 → 9](#level-8--9) 
#### Text processing & encoding (9–13) 
* [Level 9 → 10](#level-9--10) 
* [Level 10 → 11](#level-10--11) 
* [Level 11 → 12](#level-11--12) 
* [Level 12 → 13](#level-12--13) 
 #### SSH keys & networking (13–17) 
* [Level 13 → 14](#level-13--14) 
* [Level 14 → 15](#level-14--15) 
* [Level 15 → 16](#level-15--16) 
* [Level 16 → 17](#level-16--17) 
#### Comparison & remote execution (17–19) 
* [Level 17 → 18](#level-17--18) 
* [Level 18 → 19](#level-18--19) 
#### Processes & scheduling (20–24) 
* [Level 19 → 20](#level-19--20) 
* [Level 20 → 21](#level-20--21) 
* [Level 21 → 22](#level-21--22) 
* [Level 22 → 23](#level-22--23) 
* [Level 23 → 24](#level-23--24) 
#### Scripting& git & escapes (24–33) 
* [Level 24 → 25](#level-24--25) 
* [Level 25 → 26](#level-25--26) 
* [Level 26 → 27](#level-26--27) 
* [Level 27 → 28](#level-27--28) 
* [Level 28 → 29](#level-28--29) 
* [Level 29 → 30](#level-29--30) 
* [Level 30 → 31](#level-30--31) 
* [Level 31 → 32](#level-31--32) 
* [Level 32 → 33](#level-32--33)

---
## Level 0 → 1

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit0 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** find the password for level 1, which is stored inside a `readme` file in the home directory.

**Concept:** basic navigation — `ls` to list files, `cat` to print a file's content.

**Solution:**
```bash
bandit0@bandit:~$ ls
readme

bandit0@bandit:~$ cat readme
Congratulations on your first steps into the bandit game!!
The password you are looking for is: <PASSWORD>
```

---

## Level 1 → 2

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit1 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** read a file that is literally named `-` (a single dash).

**Concept:** a dash is a reserved symbol for most commands (it usually means "read from stdin" or is treated as a flag). To force the command to treat it as a real filename, you give it a **path** to the file instead of the bare name — that way the command can't confuse it with an option.

**Solution:**
```bash
bandit1@bandit:~$ ls
-

bandit1@bandit:~$ cat ./-
<PASSWORD>
```
`./-` means "the file named `-` inside the current directory (`.`)". Because it's a path and not a bare `-`, `cat` reads it correctly.

---

## Level 2 → 3

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit2 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** read a file named `--spaces in this filename--`.

**Concept:** spaces inside a filename get interpreted by the shell as separators between multiple arguments, unless you escape them. Typing the first character and pressing **Tab** lets the shell auto-complete the name and automatically insert the escape characters (backslashes) for you.

**Solution:**
```bash
bandit2@bandit:~$ ls
--spaces in this filename--

bandit2@bandit:~$ cat ./--spaces\ in\ this\ filename--
<PASSWORD>
```

---

## Level 3 → 4

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit3 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** find a hidden file inside the `inhere` directory.

**Concept:** in Linux, any file or directory starting with a dot (`.`) is considered "hidden" and won't show up with a plain `ls`. Useful `ls` flags:
- `-l` → long/detailed listing
- `-h` → human-readable sizes
- `-a` → show **all** files, including hidden ones

**Solution:**
```bash
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls -lah
total 12K
drwxr-xr-x 2 root    root    4.0K Jun 24 14:59 .
drwxr-xr-x 3 root    root    4.0K Jun 24 14:59 ..
-rw-r----- 1 bandit4 bandit3   33 Jun 24 14:59 ...Hiding-From-You

bandit3@bandit:~/inhere$ cat ...Hiding-From-You
<PASSWORD>
```

---

## Level 4 → 5

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit4 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** find the one human-readable file among ten files (`-file00` … `-file09`) inside `inhere`.

**Concept:** since all filenames start with `-`, we again need paths to reference them. To check the type of many files at once, use the `file` command with a wildcard (`*`), which matches "anything after this point". This avoids running `file` on each one manually.

**Solution:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit4 bandit@bandit.labs.overthewire.org -p 2220

bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09

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
<PASSWORD>
```
`file` tells you the type of content, and `ASCII text` means plain human-readable text.

---

## Level 5 → 6

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit5 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** find one file among many nested directories that is:
- human-readable
- exactly 1033 bytes
- NOT executable

**Concept:** `find` searches recursively through directories and can filter by multiple properties at once:
- `-type f` → only regular files
- `-size 1033c` → exact size in bytes (`c` = bytes)
- `! -executable` → NOT executable

**Solution:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit5 bandit@bandit.labs.overthewire.org -p 2220

bandit5@bandit:~$ ls 
inhere

bandit5@bandit:~$ cd inhere/

bandit5@bandit:~/inhere$ ls
maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17

bandit5@bandit:~/inhere$  find . -type f -size 1033c ! -executable
./maybehere07/.file2

bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
<PASSWORD>
```

---

## Level 6 → 7

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit6 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** find a file somewhere on the **entire filesystem** (not just the home directory) that is:
- owned by user `bandit7`
- owned by group `bandit6`
- exactly 33 bytes

**Concept:** `/` is the root of the filesystem, so `find /` searches everywhere. Since we don't have permission to read many system directories, `find` throws a lot of "Permission denied" errors on file descriptor `2` (stderr). We can silence these by redirecting stderr to `/dev/null` — a special "black hole" device that discards anything written to it.

**Solution:**
```bash
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password

bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
<PASSWORD>
```

---

## Level 7 → 8

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit7 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** the password sits on the same line as the word `millionth` inside a huge text file.

**Concept:** `grep` filters lines of text that match a pattern. Piping (`|`) sends the output of one command as the input of the next.

**Solution:**
```bash
bandit7@bandit:~$ cat data.txt | grep millionth
millionth	<PASSWORD>
```

---

## Level 8 → 9

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit8 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** find the one line in the file that appears exactly once.

**Concept:** `uniq -u` only compares a line to its **immediate neighbors**, so it only works correctly on **sorted** input. Since the file isn't sorted, we must `sort` it first, then pipe into `uniq -u`.

**Solution:**
```bash
bandit8@bandit:~$ ls 
data.txt

bandit8@bandit:~$ wc -l data.txt 
1001 data.txt

bandit8@bandit:~$ cat data.txt| uniq -u | head
tob2Ifz9ZpTlahbsHpV9rHyxKYV50E6d
b5l3vW4lfE58gjIRcgZmRgOQ3L7LL4rE
TbJy4tkWD7DM0ImHuy0AM5LdDee0kx7d
7GeeWiLeZOXFxt4V5fuEo3JjOJU73ByA
zlVs1t1ZAwNkYoJeu2keu1XDb379Enps

bandit8@bandit:~$ cat data.txt | sort | uniq -u
<PASSWORD>
```

---

## Level 9 → 10

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit9 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** find a human-readable password inside a file that's mostly binary garbage, next to a run of `=` characters.

**Concept:** `cat` on binary data is unreadable. `strings` extracts only sequences of printable characters (3+ chars by default) from a file, human-readable or not.

**Solution:**
```bash
bandit9@bandit:~$ strings data.txt | grep "=="
========== password
>========== is
R========== <PASSWORD>
```

---

## Level 10 → 11

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit10 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** decode a Base64-encoded string.

**Concept:** `base64 -d` decodes Base64 text back into its original form.

**Solution:**
```bash
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIH.....== #I will not appear it all to save passowrd secret

bandit10@bandit:~$ base64 -d data.txt
The password is <PASSWORD>
```

---

## Level 11 → 12

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit11 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** decode text that has been rotated by 13 letters (ROT13) — `A` becomes `N`, `M` becomes `Z`, etc.

**Concept:** `tr` translates characters from one set to another. It also accepts ranges, so instead of writing out all 26 letters we can just say "map `A-Z`/`a-z` onto `N-Z,A-M`/`n-z,a-m`". No online tool is needed (and using one would leak the password to a third party).

**Solution:**
```bash
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is <PASSWORD>
```

---

## Level 12 → 13

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit12 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** the password is buried inside a file that's been compressed multiple times in a row, and the file itself is a hex dump of the actual binary data.

**Concept:**
- `xxd -r` reverses a hex dump back into the original binary bytes.
- `file` identifies the compression type of the current binary.
- Repeat: rename with the matching extension → decompress → check `file` again → repeat, until the file type is `ASCII text`.

**Solution:**
```bash
bandit12@bandit:~$ mkdir /tmp/karam_comp && cp data.txt /tmp/karam_comp/ && cd /tmp/karam_comp

bandit12@bandit:~$ ls
 data.txt
bandit12@bandit:~$ mkdir /tmp/karam_comp
bandit12@bandit:~$ cp data.txt /tmp/karam_comp/
bandit12@bandit:~$ cd /tmp/karam_comp
bandit12@bandit:/tmp/karam_comp$ ls
 data.txt
bandit12@bandit:/tmp/karam_comp$ file data.txt 
 data.txt: ASCII text
bandit12@bandit:/tmp/karam_comp$ head data.txt 
 00000000: 1f8b 0808 b2f0 3b6a 0203 6461 7461 322e  ......;j..data2.
 00000010: 6269 6e00 0142 02bd fd42 5a68 3931 4159  bin..B...BZh91AY
 00000020: 2653 59dc 0966 8300 001a ffff dff5 c5fe  &SY..f..........
 00000030: b8ef a7be bddb f8a7 febb ffc9 bfbf 9fbf  ................
 00000040: b77b bfff fbd9 7ffe 5fef efcf b001 3b19  .{......_.....;.
 00000050: 9206 87a9 a068 0340 3400 341a 1a1a 0340  .....h.@4.4....@
 00000060: 1a68 068d 1a00 0646 8000 0610 0d00 069a  .h.....F........
 00000070: 0640 683c a0d0 3d43 4d3d 4f51 b420 0680  .@h<..=CM=OQ. ..
 00000080: d034 0000 0079 41a3 40d1 ea00 0f48 000d  .4...yA.@....H..
 00000090: 1a34 d1ea 7a83 d468 f441 a03d 469a 3400  .4..z..h.A.=F.4.
 # convert the hexdump back into real binary
bandit12@bandit:/tmp/karam_comp$ xxd -r data.txt data.out
bandit12@bandit:/tmp/karam_comp$ file data.out 
 data.out: gzip compressed data, was "data2.bin", last modified: Wed Jun 24 14:58:58 2026, max compression, from Unix, original size modulo 2^32 578

# repeat: rename with the right extension, then decompress, then check "file" again
-----------------------------------------------------
bandit12@bandit:/tmp/karam_comp$ mv data.out data.gz
bandit12@bandit:/tmp/karam_comp$ gzip -d data.gz 
bandit12@bandit:/tmp/karam_comp$ ls
 data  data.txt
bandit12@bandit:/tmp/karam_comp$ file data
 data: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/karam_comp$ mv data data.bz2
bandit12@bandit:/tmp/karam_comp$ bzip2 -d data.bz2 
bandit12@bandit:/tmp/karam_comp$ ls
 data  data.txt
bandit12@bandit:/tmp/karam_comp$ file data
 data: gzip compressed data, was "data4.bin", last modified: Wed Jun 24 14:58:58 2026, max compression, from Unix, original size modulo 2^32 20480
bandit12@bandit:/tmp/karam_comp$ mv data data.gz
bandit12@bandit:/tmp/karam_comp$ gzip -d data.gz 
bandit12@bandit:/tmp/karam_comp$ ls 
 data  data.txt
bandit12@bandit:/tmp/karam_comp$ file data
 data: POSIX tar archive (GNU)
bandit12@bandit:/tmp/karam_comp$ mv data data.tar
bandit12@bandit:/tmp/karam_comp$ tar -xvf data.tar 
 data5.bin
bandit12@bandit:/tmp/karam_comp$ file data5.bin 
 data5.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/karam_comp$ mv data5.bin data5.tar
bandit12@bandit:/tmp/karam_comp$ tar -xvf data5.tar 
 data6.bin
bandit12@bandit:/tmp/karam_comp$ file data6.bin 
 data6.bin: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/karam_comp$ mv data6.bin data6.bz2
bandit12@bandit:/tmp/karam_comp$ bzip2 -d data6.bz2 
bandit12@bandit:/tmp/karam_comp$ ls
 data.tar  data.txt  data5.tar  data6
bandit12@bandit:/tmp/karam_comp$ file data6
 data6: POSIX tar archive (GNU)
bandit12@bandit:/tmp/karam_comp$ mv data6 data6.tar
bandit12@bandit:/tmp/karam_comp$ tar -xvf data6.tar 
 data8.bin
bandit12@bandit:/tmp/karam_comp$ file data8.bin 
 data8.bin: gzip compressed data, was "data9.bin", last modified: Wed Jun 24 14:58:58 2026, max compression, from Unix, original size modulo 2^32 49
bandit12@bandit:/tmp/karam_comp$ mv data8.bin data8.gz
bandit12@bandit:/tmp/karam_comp$ gzip -d data8.gz 
bandit12@bandit:/tmp/karam_comp$ ls
 data.tar  data.txt  data5.tar  data6.tar  data8
 ---------------------------------------------------
# ...keeps repeating through tar / bzip2 / gzip layers...
bandit12@bandit:/tmp/karam_comp$ file data8
data8: ASCII text
bandit12@bandit:/tmp/karam_comp$ cat data8
The password is <PASSWORD>
```

---

## Level 13 → 14

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit13 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** an SSH private key for bandit14 is sitting in the home directory — use it to log in instead of a password.

**Concept:** `ssh -i <keyfile>` authenticates using a private key instead of a password. Since we don't own the key, SSH may also require the permissions to be restrictive (e.g. `chmod 600`) before it will accept it.

**Solution:**
```bash
bandit13@bandit:~$ ls
sshkey.private
# we can take the ssh private key and login with it
#no need for password and take it in anyway you want even cope paste
bandit13@bandit:~$ cat sshkey.private 
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAA
.....
KN158egNsB+sEAAAAOcnVkeUBsb2NhbGhvc3QBAgMEBQ==
-----END OPENSSH PRIVATE KEY-----
#exit the session and login with next level to get the password
bandit13@bandit:~$ exit
logout
#logging in using the key
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit14 -i bandit13.sshkey bandit0@bandit.labs.overthewire.org -p 2220 
#here we can get the password 
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
<PASSWORD>
```

---

## Level 14 → 15

**Goal:** submit the current password to a listening service on `localhost:30000` to receive the next one.

**Concept:** `nc` (netcat) opens a raw TCP connection. Piping the password into it sends it as the payload of the connection.

**Solution:**
```bash
#since we already logged in from the previous level 
#we can make a connection using nc 
bandit14@bandit:~$ nc localhost 30000 -v
Connection to localhost (127.0.0.1) 30000 port [tcp/*] succeeded!
<PASSWORD - bandit14>
Correct!
<PASSWORD - bandit15>
```
The service replies with the password for bandit15.

---

## Level 15 → 16

**Login:**
```
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit15 bandit@bandit.labs.overthewire.org -p 2220   
```
**Goal:** same idea as level 14, but the service on port `30001` uses SSL/TLS encryption.

**Concept:** plain `nc` can't speak TLS, so we use `openssl s_client` instead, which can establish an encrypted connection. `-quiet` suppresses the verbose handshake/certificate output so we only see the actual response.

**Solution:**
```bash
bandit15@bandit:~$ openssl s_client -connect localhost:30001 -quiet
'Connecting to 127.0.0.1
Cant use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1'
<PASSWORD - bandit15>
Correct!
<PASSWORD - bandit16>
```

---

## Level 16 → 17

**Login:**
```
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit16 bandit@bandit.labs.overthewire.org -p 2220
```

**Goal:** find which port in the range `31000-32000` gives us a private key for the next level.

**Concept:** `nmap` scans a range of ports to see which are open. Once the right port is found, we connect to it we used `-sV` to see the services and connect to the right port we need (31790).

**Solution:**
```bash
bandit16@bandit:~$ nmap -sV localhost -p 31000-32000
Starting Nmap 7.98 ( https://nmap.org ) at 2026-07-08 14:36 +0000
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00014s latency).
Other addresses for localhost (not scanned): ::1
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo

bandit16@bandit:~$ openssl s_client -connect localhost:31790 -quiet
Connecting to 127.0.0.1
Cant use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
Correct!
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAA
....
Pfos/2C+rbNuHjAAAADnJ1ZHlAbG9jYWxob3N0AQIDBA==
-----END OPENSSH PRIVATE KEY-----
```
Copy the key into a file (e.g. `bandit17.sshkey`), then restrict its permissions to 700 so SSH will accept it instead of falling back to password auth:
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit17 -i bandit17.sshkey bandit0@bandit.labs.overthewire.org -p 2220

bandit17@bandit:~$ cat /etc/bandit_pass/bandit17
<PASSWORD>
```

---

## Level 17 → 18

**Goal:** the home directory has `passwords.old` and `passwords.new` — the password changed between the two, and we need to find which line differs.

**Concept:** `diff` compares two files line by line and shows what changed.

**Solution:**
```bash
bandit17@bandit:~$ ls
passwords.new  passwords.old
bandit17@bandit:~$ diff passwords.old passwords.new 
42c42
< <PASSWORD - bandit17>
---
> <PASSWORD - bandit18>
```

---

## Level 18 → 19

**Login:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit18  bandit0@bandit.labs.overthewire.org -p 2220
```
**Goal:** logging in normally kicks you out immediately, because `.bashrc` contains a command that exits the session as soon as you log in.

**Concept:** SSH lets you append a command directly to the login command. That command runs *before* `.bashrc`'s logout logic takes effect, since it replaces the default shell startup with your one-off command.

**Solution:**
```
....
  For support, questions or comments, contact us on discord or IRC.

  Enjoy your stay!

Byebye !
Connection to bandit.labs.overthewire.org closed.
```

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 'cat readme'

bandit18@bandit.labs.overthewire.orgs password: 
<PASSWORD>

```

---

## Level 19 → 20

**Login:**
```
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit19 bandit0@bandit.labs.overthewire.org -p 2220   
```
**Goal:** there's a SetUID binary (`bandit20-do`) in the home directory. A SetUID binary runs with the *file owner's* privileges rather than the privileges of whoever executes it — here, that means it runs as bandit20.

**Concept:** running the binary with a command as an argument lets you read files bandit20 can read but bandit19 can't.

**Solution:**
```bash
bandit19@bandit:~$ ls
bandit20-do

bandit19@bandit:~$ ./bandit20-do 
Run a command as another user.
  Example: ./bandit20-do whoami

bandit19@bandit:~$ ls -lah bandit20-do 
-rwsr-x--- 1 bandit20 bandit19 15K Jun 24 14:59 bandit20-do

bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
<PASSWORD>
```

---

## Level 20 → 21

**Login:**
```
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit20 bandit0@bandit.labs.overthewire.org -p 2220 
```
**Goal:** there is a SetUID program (`suconnect`) that connects to a port you give it, reads a password from that connection, and — if it's correct — sends back the next level's password on the same connection.

**Concept:** open a listener with `nc -l -p <port>` in one terminal (or one `tmux` pane), then run the SetUID binary pointing at that same port from another terminal. Type your current password into the listener; `suconnect` reads it, validates it, and writes the next password back to the same connection.

**Solution:**
```bash
# terminal 1 - listener
bandit20@bandit:~$ nc -l -p 12345

# terminal 2 (or another tmux pane) - run the SetUID helper against the same port
bandit20@bandit:~$ ./suconnect 12345

# back in terminal 1, type the current password and press enter
<current-password>
# suconnect validates it and sends the next password back to terminal 1
<PASSWORD>
```

---

## Level 21 → 22

**Goal:** find a password left behind by a cron job.

**Concept:** cron jobs are scheduled tasks defined in `/etc/cron.d/`. Reading the job files there shows what script runs and how often. Following that script to where it writes its output reveals the password.

**Cron syntax refresher** (five fields before the command):
```
* * * * *  command
│ │ │ │ │
│ │ │ │ └── day of week (0-7)
│ │ │ └──── month (1-12)
│ │ └────── day of month (1-31)
│ └──────── hour (0-23)
└────────── minute (0-59)
```

**Solution:**
```bash
bandit21@bandit:~$ cd /etc/cron.d/
bandit21@bandit:/etc/cron.d$ ls
'behemoth4_cleanup  clean_tmp  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  e2scrub_all  leviathan5_cleanup  manpage3_resetpw_job  otw-tmp-dir'

bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
'@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null'

bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
'#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv'

bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
<PASSWORD>

```

---

## Level 22 → 23

**Login:**
```
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit22 bandit0@bandit.labs.overthewire.org -p 2220 
```
**Goal:** similar cron job, but this time the output filename is the MD5 hash of a known string rather than a fixed name.

**Concept:** the script computes `md5sum` of a string (like `"I am user bandit23"`) and uses that hash as the filename. We can just run the same command ourselves to predict the filename.

**Solution:**
```bash
bandit22@bandit:~$ cd /etc/cron.
'cron.d/       cron.daily/   cron.hourly/  cron.monthly/ cron.weekly/  cron.yearly/'
bandit22@bandit:~$ cd /etc/cron.d/
bandit22@bandit:/etc/cron.d$ ls
'behemoth4_cleanup  clean_tmp  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  e2scrub_all  leviathan5_cleanup  manpage3_resetpw_job  otw-tmp-dir'
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23 
'@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null'
bandit22@bandit:/etc/cron.d$ cat bandit23 '/usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget'
bandit22@bandit:/etc/cron.d$ myname=bandit23
bandit22@bandit:/etc/cron.d$ echo $myname
'bandit23'
bandit22@bandit:/etc/cron.d$ echo I am user $myname | md5sum | cut -d ' ' -f 1
'8ca319486bfbbc3663ea0fbe81326349'
bandit22@bandit:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
<PASSWORD>
```

---

## Level 23 → 24

**Goal:** a cron job run as bandit24 executes any script it finds in a "foo" folder, then deletes it. We can drop our own script there to get it executed as bandit24.

**Concept:** because the cron job runs as bandit24, whatever script we place there can read files only bandit24 has access to — like its own password file.

**Solution:**
```bash
bandit23@bandit:~$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

shopt -s nullglob

myname=$(whoami)

cd /var/spool/"$myname"/foo || exit 
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" "./$i")"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi
done
```

```bash
bandit23@bandit:/tmp$ nano karam.sh
bandit23@bandit:/tmp$ mkdir karam24
bandit23@bandit:/tmp/karam24$ touch output.txt
bandit23@bandit:/tmp/karam24$ cp ../karam.sh /var/spool/bandit24/foo/
# wait a minute for cron to run it
bandit23@bandit:/tmp/karam24$ cat output.txt 
<PASSWORD>
```

```bash
# the script that in karam.sh file
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/karam24/output.txt
```

---

## Level 24 → 25

**Goal:** a service on port `30002` accepts the current password plus a 4-digit PIN, and tells us if the PIN is wrong — we need to brute-force all 10,000 combinations.

**Concept:** generate every possible PIN (`0000`-`9999`), pair each with the known password, send them all through the connection in one go, then filter out the "Wrong!" responses to find the one that succeeded.

**Solution:**
```bash
bandit24@bandit:~$ nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 0000
Wrong! Please enter the correct current password and pincode. Try again.
03
Wrong! Please enter the correct current password and pincode. Try again.
234
Wrong! Please enter the correct current password and pincode. Try again.
6
```

```bash
#!/bin/bash
mkdir /tmp/karam_solve
touch /tmp/karam_solve/PINs.txt
touch /tmp/karam_solve/rightPIN.txt
touch /tmp/karam_solve/nc_output.txt

# Generate the PINs from 0000 to 9999 each line with the password and pin beside it 
for i in {0000..9999}
do
        echo hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv $i >> /tmp/karam_solve/PINs.txt
done
#make file containing all the output from the connection with port 30002 the wrong and the correct 
cat /tmp/karam_solve/PINs.txt | nc localhost 30002  > /tmp/karam_solve/nc_output.txt

#after recognizing the wrong output we want to grep anything that's not corect or the first lines of the connection to get the right one
o=$(cat /tmp/karam_solve/nc_output.txt | grep -v "Wrong" | grep -v "I am the pincode checker")

#get the last line for the correct answer and put it into a variable , but the isseue is that the correct answer are 4 lines in total 
x=$(wc -l /tmp/karam_solve/nc_output.txt | uniq -u |cut -d ' ' -f 1) 

#the output for the correct answer with the password 
echo "|"
echo "|"
echo "|"
echo "========================="
echo "the output for the right answer is :"
echo $o
echo "=========================="
#save the right line from pins file and decrease 3 to get the first line so it contains the connection
pinline=$((x - 3))

#put the output for the right line that have a pin in the rightpin file 
sed -n "${pinline}p" /tmp/karam_solve/PINs.txt > /tmp/karam_solve/rightPIN.txt

#the output for the previous password with the exact pin
echo "|"
echo "|"
echo "|"
echo "=========================="
echo "your previous password with the right PIN number is : "
cat /tmp/karam_solve/rightPIN.txt
echo "============================"
echo "|"
echo "|"
echo "|"
echo "and you can find the datials here :"
echo "all PINs      : /tmp/karam_solve/PINs.txt"
echo "all outputs   : /tmp/karam_solve/nc_output.txt"
echo "the right PIN : /tmp/karam_solve/rightPIN.txt"
```

```bash
|
|
=========================
the output for the right answer is :
Correct! The password of user bandit25 is SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
==========================
|
|
|
==========================
your previous password with the right PIN number is : 
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 3976
============================
|
|
|
and you can find the datials here :
all PINs      : /tmp/karam_solve/PINs.txt
all outputs   : /tmp/karam_solve/nc_output.txt
the right PIN : /tmp/karam_solve/rightPIN.txt
```
The surviving line contains the next password.

---

## Level 25 → 26

**Goal:** bandit26's login shell isn't `/bin/bash` — it's a custom program (`showtext`) that opens a pager (`more`) on a text file and then exits, kicking us out before we ever get a real shell.

**Concept:** if the terminal window is small enough, `more` will pause mid-file waiting for input instead of running to completion instantly. From inside `more`, pressing `v` opens the file in `vi`. From `vi`, you can spawn a shell with:
```
:set shell=/bin/bash
:shell
```

**Solution:**
1. Shrink your terminal window so the text doesn't finish scrolling instantly.
2. Log in with bandit26's private key.
3. While `more` is paused, press `v` to jump into `vi`.
4. In `vi`, type `:set shell=/bin/bash` then `:shell` to drop into a real bash shell.
5. Resize the window back to normal, then read the password:
```bash
bandit26@bandit:~$ cat /etc/bandit_pass/bandit26
<PASSWORD>
```

---

## Level 26 → 27

**Goal:** from the shell obtained in the previous level, find an executable in bandit27's home directory to escalate further.

**Concept:** listing the home directory reveals a SetUID/SetGID helper binary — running it drops you into a shell as bandit27.

**Solution:**
```bash
bandit26@bandit:~$ ls -la
bandit26-do

bandit26@bandit:~$ ./bandit26-do bash
bandit27@bandit:~$ cat /etc/bandit_pass/bandit27
<PASSWORD>
```

---

## Level 27 → 28

**Goal:** clone a Git repository hosted on the game server and read its README.

**Concept:** `git clone` over SSH, using the level's own port.

**Solution:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo

bandit27@bandit:~$ cat /repo/README
<PASSWORD>
```

---

## Level 28 → 29

**Goal:** the README says the password isn't shown directly anymore — it needs to be found in the repository's commit history.

**Concept:** `git log -p` shows the full diff (patch) of every commit, including content that was later removed.

**Solution:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo

┌──(karam03 ♛ HACKER)-[~]
└─$  cd /repo

┌──(karam03 ♛ HACKER)-[~]
└─$  git log -p
# an earlier commit's diff reveals the password before it was removed
```

---

## Level 29 → 30

**Goal:** the current README says the password isn't included "in production" — implying another branch might still have it.

**Concept:** `git branch -a` lists all branches (including remote ones); `git checkout <branch>` switches to one.

**Solution:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo

┌──(karam03 ♛ HACKER)-[~]
└─$  cd /repo

┌──(karam03 ♛ HACKER)-[~]
└─$  git branch -a

┌──(karam03 ♛ HACKER)-[~]
└─$  git checkout dev

┌──(karam03 ♛ HACKER)-[~]
└─$  cat README
<PASSWORD>
```

---

## Level 30 → 31

**Goal:** no branch or commit history seems to hold the password this time.

**Concept:** Git tags can also carry hidden data. `git tag` lists them, and `git show <tag>` reveals the tagged content.

**Solution:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo

┌──(karam03 ♛ HACKER)-[~]
└─$  cd /repo

┌──(karam03 ♛ HACKER)-[~]
└─$  git tag
secret

bandit30@bandit:~$ git show secret
<PASSWORD>
```

---

## Level 31 → 32

**Goal:** the repo instructions require committing a specific file with specific content and pushing it, to unlock the next password.

**Concept:** create the exact file requested (e.g. `key.txt` with the content asked for), `git add -f` to force-add it if it's gitignored, commit, and push.

**Solution:**
```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo

┌──(karam03 ♛ HACKER)-[~]
└─$  cd /repo

┌──(karam03 ♛ HACKER)-[~]
└─$ echo "May I come in?" > key.txt

┌──(karam03 ♛ HACKER)-[~]
└─$ git add -f key.txt

┌──(karam03 ♛ HACKER)-[~]
└─$ git commit -m "add key"

┌──(karam03 ♛ HACKER)-[~]
└─$ git push origin master
# the push output / response reveals the password
```

---

## Level 32 → 33

**Goal:** the shell only understands UPPERCASE commands, so lowercase commands don't run.

**Concept:** `$0` refers to the name of the currently running shell/process. Typing `$0` re-invokes the current shell as a plain command, which drops you into a normal, lowercase-friendly bash shell instead of the restricted uppercase one.

**Solution:**
```bash
bandit32@bandit:~$ $0
bandit33@bandit:~$ cat /etc/bandit_pass/bandit33
<PASSWORD>
```

---

DONE BY KARAM
