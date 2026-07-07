# OverTheWire: Bandit Writeups

Welcome to my writeups for the [OverTheWire Bandit wargame](https://overthewire.org/wargames/bandit/). 

Bandit is designed for absolute beginners to learn the basics of the Linux command line and security concepts. In this repository, I document my journey through the levels, explaining the tools, concepts, and commands used to solve each challenge.

## ⚠️ Disclaimer
OverTheWire requests that players do not publish the passwords to the levels. In the spirit of the game, my writeups will guide you through the exact commands and logic needed to find the password yourself, but the actual passwords are redacted.

## Table of Contents

### Levels 0 - 9
* [Level 0 -> Level 1](#level 1 -> 2)
* [Level 1 -> Level 2](./Level_00-09/Level_01-02.md)
...

### Levels 10 - 19
* [Level 10 -> Level 11](./Level_10-19/Level_10-11.md)
...

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

## Level 1 -> 2
*login command :* 
`ssh -l bandit1 bandit@bandit.labs.overthewire.org -p 2220`
the password we already found in the previous level 

so in this level we should read a file that name is a dash `-` so all we should do is the same `cat` that we used before **but** using the same file name as it set is **WRONG** because the dash is a reserved symbol for the `cat` command , instead of using the same file name we should use the file name with it's path so `cat` could know that this is a file name because we used a path to reach it so the right command is : 
`cat ./-` and the dot is where we are right now so i tell the command that just open the file that name is dash inside the directory that i am already in 
and we can get the new password from the file 

```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit1 bandit@bandit.labs.overthewire.org -p 2220

bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat ./-
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

## Level 2 -> 3
*login command :*
`ssh -l bandit2 bandit@bandit.labs.overthewire.org -p 2220`
the password we already found in the previous level

so the file we are looking for is `--spaces in this filename--` and as we said about reserved symbols we should use path , but here we used the path but if we typed the `spaces` that in the file name itself , the `cat` command will see is a separated files and it will not be capable of reading it , we can solve this by typing the first letter or symbol the file name and press `tap` button on the keyboard so it can be completed automatically and here we saw that it completed by typing `\` slash before the space to avoid  the separation .
```bash 
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit2 bandit@bandit.labs.overthewire.org -p 2220

bandit2@bandit:~$ ls
--spaces in this filename--
bandit2@bandit:~$ cat ./--spaces\ in\ this\ filename-- 
XXXXXXXXXXXXXXXXXXXXX
```

## Level 3 -> 4
*login command :*
`ssh -l bandit3 bandit@bandit.labs.overthewire.org -p 2220`
the password we already found in the previous level

so here basecally the challenge tells us that there is a **hidden** file inside `inhere` directory so we should move into the `inhere` directory using `cd` command and see what is this directory contains using `ls` command and we should know the options for the `ls` command and what can reveal the **hidden** files for us 
- -l : this can list the items for the files for us 
- -h : this is for human readable
- -a : that's the one we need so this option can show us all the files including the **hidden** files that start with dot ( . ) in their names .
so we can use `cat` command and can tell us wahts the password for the next level .

```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit3 bandit@bandit.labs.overthewire.org -p 2220
bandit3@bandit:~$ ls
inhere

bandit3@bandit:~$ cd inhere/

bandit3@bandit:~/inhere$ ls

bandit3@bandit:~/inhere$ ls -lah
total 12K
drwxr-xr-x 2 root    root    4.0K Jun 24 14:59 .
drwxr-xr-x 3 root    root    4.0K Jun 24 14:59 ..
-rw-r----- 1 bandit4 bandit3   33 Jun 24 14:59 ...Hiding-From-You

bandit3@bandit:~/inhere$ cat ...Hiding-From-You 
XXXXXXXXXXXXXXXXXXXXX
```

## Level 4 -> 5
*login command :*
`ssh -l bandit4 bandit@bandit.labs.overthewire.org -p 2220`
the password we already found in the previous level

so in this challenge , we have multiple of files inside `inhere` directory and there is just one that is human readable file so we should go to `inhere` directory and show the content of this directory using `ls` and it shows multiple of files that begins with `-` *dash* in their name 
 $-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09$ 
as we learned we should use the path for it to read , but we first should know the file type using `file` command and if there are more files than this we cannot use `file` command to see each one of them so basecally the files names are begins with `-file0` and the second digits is the digit that is changes between each file name , so w can put this `./-file0*` and the `*` in this case tells the command that run on every file that begins with file `./-file0` and it does not matter what is the rest so the `file` command will run on all the files .
then we should see the file that is readable , we can see that there is a file that is **ASCII**  [`click to read about ASCII`](https://www.ascii-code.com/)  
then we knew that the this is the readable file , when we `cat` the file we should get the password for the next level 

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
XXXXXXXXXXXXXXXXXXXXXXXXX
```

## Level 5 -> 6
*login command :*
`ssh -l bandit5 bandit@bandit.labs.overthewire.org -p 2220`
the password we already found in the previous level

so in this level we should find a file between multiple directories and multiple files , but this file has a specific properties as the challenge mentioned :
-  human-readable 
- 1033 bytes in size
- not executable

so we should use the `find` command to find something between multiple things 
the type command has a lot of options and we will use the following :
- `-type` : so we can specify the type for the something that we need 
- `-size`: so we can specify the size for the file we are looking for 
- `-executable`: so we can tell the command to find something executable or not 

in that case we are looking for a `type` that is 'file' so `-type f` ,  and we are looking for a file that it's size is 1033 bytes so opcion '**c**' is for bytes as we saw in manual so `-size 1033c` , and we are looking for something that is not executable so `! -executable`  and we found it, `cat` i to see the next password level .


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
XXXXXXXXXXXXXXXXXXXXXXX
```

## Level 6 -> 7
*login command :*
`ssh -l bandit6 bandit@bandit.labs.overthewire.org -p 2220`
the password we already found in the previous level

in this challenge we should find for a file that is on the **server** , they didn't mentioned anything about a specific directory so we should use `find` command again but this time on the server not the current directory and the symbol that means the you are in the root directory or the most upper directory that contains everything is slash `/` , and we have properties that we are loking for :
- owned by user bandit7
- owned by group bandit 6
- 33 bytes size

so we should look for the file in these properties , using `-group` to find the right group , and using `-size` to look for the size we need so `-size 33c` .
this command will give us a lot of permission denied so the number that for the errors is number ***2*** so we now want to send these errors to somewhere to never see them , so the right directory is `/dev/null`  this directory have a trash values so we don't need anything from this directory and we can send these error to it so `2>/dev/null` 
now we found the file , we can `cat` it and take the password for the next level.

```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit6 bandit@bandit.labs.overthewire.org -p 2220

bandit6@bandit:~$ find / -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password

bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
XXXXXXXXXXXXXXXXXXXXXX
```

## Level 7 -> 8
*login command :*
`ssh -l bandit7 bandit@bandit.labs.overthewire.org -p 2220`
the password we already found in the previous level

in this level we should find the password that stored next to the word "millionth"
we first used `wc -l` to find how many lines that the file contains and saw that there are a lot of lines so we `cat` the file but using `grep` , so `grep` is a filtering tool that can find anything inside the file , so we `cat` the file and use the pipe `|` to make the first output go to the second input which is `grep` in this case 
the `grep` found the word and the password next to it .

```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit7 bandit@bandit.labs.overthewire.org -p 2220

bandit7@bandit:~$ ls
data.txt

bandit7@bandit:~$ wc -l data.txt 
98567 data.txt

bandit7@bandit:~$ cat data.txt | grep millionth
millionth	XXXXXXXXXXXXXXXXXXXXXXXX
```

## Level 8 -> 9
*login command :*
`ssh -l bandit8 bandit@bandit.labs.overthewire.org -p 2220`
the password we already found in the previous level

in this level we should find the uniq line that occurs once , wo the file also have a lot of lines so when we should use `uniq` command but the issue is the `uniq` command give you the unique line of text comparing with it's adjacent , in this case we cannot use it alone because the lines are not ordered or sorted so the output will give me all the lines , so we should use `sort` command to sort the lines and then use the `uniq` command to compare the lines with their adjacent and give me the final output which is the password for the next level.

```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit8 bandit@bandit.labs.overthewire.org -p 2220

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
XXXXXXXXXXXXXXXXXXXX

```

## Level 9 -> 10
*login command :*
`ssh -l bandit9 bandit@bandit.labs.overthewire.org -p 2220`
the password we already found in the previous level

in this level the password is next to several **=** and it's a human readable , `cat` will not be useful because it shows a text either human readable or not , in this case we will use `strings` command because this command shows the human readable with at least 3 characters per line or per a single text , then use `grep` command to find the `=` because the password is next to it .


```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit9 bandit@bandit.labs.overthewire.org -p 2220

bandit9@bandit:~$ ls 
data.txt

bandit9@bandit:~$ strings data.txt | grep "==="
cL0========== the
========== password
>========== is
R========== XXXXXXXXXXXXXXXXXXXXXX
```

## Level 10 -> 11
*login command :*
`ssh -l bandit10 bandit@bandit.labs.overthewire.org -p 2220`
the password we already found in the previous level

in this challenge we should decode the string to find out what is the password.
it's mentioned that it's a base64 encode and we have a tool in linux that decode this strings it's `base64` with -d option to decode , we used it and find the password for the next level

```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit10 bandit@bandit.labs.overthewire.org -p 2220

bandit10@bandit:~$ ls 
data.txt

bandit10@bandit:~$ cat data.txt 
VGhlIHBhc3N3b3JkIGlzIHBZZk9ZNkh3VXNEajVyTDlVdnloVTdNQ212OHZONVJvCg==

bandit10@bandit:~$ base64 -d data.txt 
The password is XXXXXXXXXXXXXXXXXX
```

## Level 11 -> 12
*login command :*
`ssh -l bandit11 bandit@bandit.labs.overthewire.org -p 2220`
the password we already found in the previous level

in this challenge we should also decode the string because it's rotated 13 time for each letter , so **A becomes N and M become Z** for the capital and the small.
and we ==shouldn't== use any online tools to decode regarding to secure out data so we will do the following .
we already have a translater tool that translate and letter to another letter , and the good news is we can use it for a range of letter that means i don't have to type each ;etter with the letter that i want to translate to , i just can use a range like from `A to U` , and this tool is `tr` 
we used it as the folowing :
**`cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'`**
we told the tool that i want to change :
this range -> `A-Z` and `a-z `
with this range -> `N-Z` and `A-M` and` n-z `and `a-m`
so the A becomes N and so on 

```bash 
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit11 bandit@bandit.labs.overthewire.org -p 2220

bandit11@bandit:~$ ls
data.txt

bandit11@bandit:~$  cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is XXXXXXXXXXXXXXXX
```

## Level 12 -> 13
*login command :*
`ssh -l bandit12 bandit@bandit.labs.overthewire.org -p 2220`
the password we already found in the previous level

in this challenge we should decompress the file multiple times as mentioned in the description , when we saw the file content we saw that it's a hexdump so we want to get it back to the original form with using `xxd` and `-r` option to reverse this .
then we should `file` every time we decompress , and rename it and change the extension with the compression type :
- gzip -> .gz
- bzip2 -> bz2
- tar -> .tar
after several of decompressions we finally see that the file type is ASCII and then we `cat` it and we will find the password for the next level .

```bash
┌──(karam03 ♛ HACKER)-[~]
└─$ ssh -l bandit12 bandit@bandit.labs.overthewire.org -p 2220

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
bandit12@bandit:/tmp/karam_comp$ xxd -r data.txt data.out
bandit12@bandit:/tmp/karam_comp$ file data.out 
 data.out: gzip compressed data, was "data2.bin", last modified: Wed Jun 24 14:58:58 2026, max compression, from Unix, original size modulo 2^32 578
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
bandit12@bandit:/tmp/karam_comp$ file data8
 data8: ASCII text
bandit12@bandit:/tmp/karam_comp$ cat data8
The password is XXXXXXXXXXXXXXXXXXXXXXX
```
