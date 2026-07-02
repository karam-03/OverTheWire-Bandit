# Bandit: Levels 0 to 9

This section covers the foundational levels of OverTheWire's Bandit wargame. These levels focus on basic SSH connection, navigating the Linux file system, reading files with special characters, and using fundamental search commands.

---

## 🎯 Level 0
**Objective:** Connect to the game server using SSH.
* **Host:** `bandit.labs.overthewire.org`
* **Port:** `2220`
* **Username:** `bandit0`
* **Password:** `bandit0`

**Solution:**
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

---

## 🎯 Level 0 -> Level 1
**Objective:** The password for the next level is stored in a file called `readme` located in the home directory.

**Concepts Required:** Basic file reading.
**Commands Used:** `ls`, `cat`

**Solution:**
```bash
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
[REDACTED_PASSWORD]
```

---

## 🎯 Level 1 -> Level 2
**Objective:** The password for the next level is stored in a file named `-` located in the home directory.

**Concepts Required:** Reading files that start with a dash (which terminal commands usually interpret as a flag).
**Commands Used:** `cat`

**Solution:**
To read a file named `-`, you must specify the current directory path `./` so the `cat` command doesn't confuse the filename with an argument.
```bash
bandit1@bandit:~$ cat ./-
[REDACTED_PASSWORD]
```

---

## 🎯 Level 2 -> Level 3
**Objective:** The password for the next level is stored in a file called `spaces in this filename` located in the home directory.

**Concepts Required:** Escaping spaces in filenames or using quotes.

**Solution:**
*(Write your explanation and commands here)*

---

## 🎯 Level 3 -> Level 4
**Objective:** The password is in a hidden file in the `inhere` directory.

**Concepts Required:** Viewing hidden files.

**Solution:**
*(Write your explanation and commands here)*

---

## 🎯 Level 4 -> Level 5
**Objective:** The password is in the only human-readable file in the `inhere` directory.

**Concepts Required:** Determining file types.

**Solution:**
*(Write your explanation and commands here)*

---

## 🎯 Level 5 -> Level 6
**Objective:** The password is in a file somewhere under the `inhere` directory and has all of the following properties: human-readable, 1033 bytes in size, not executable.

**Concepts Required:** Finding files based on specific properties.

**Solution:**
*(Write your explanation and commands here)*

---

## 🎯 Level 6 -> Level 7
**Objective:** The password is stored somewhere on the server and has all of the following properties: owned by user bandit7, owned by group bandit6, 33 bytes in size.

**Concepts Required:** Searching the entire file system and discarding error messages.

**Solution:**
*(Write your explanation and commands here)*

---

## 🎯 Level 7 -> Level 8
**Objective:** The password is stored in the file `data.txt` next to the word "millionth".

**Concepts Required:** Searching for text within a file.

**Solution:**
*(Write your explanation and commands here)*

---

## 🎯 Level 8 -> Level 9
**Objective:** The password is stored in the file `data.txt` and is the only line of text that occurs only once.

**Concepts Required:** Sorting data and finding unique lines.

**Solution:**
*(Write your explanation and commands here)*

---

## 🎯 Level 9 -> Level 10
**Objective:** The password is stored in the file `data.txt` in one of the few human-readable strings, preceded by several '=' characters.

**Concepts Required:** Extracting readable strings from binary/data files.

**Solution:**
*(Write your explanation and commands here)*
