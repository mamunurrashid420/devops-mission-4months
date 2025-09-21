# Linux Command Line Cheat Sheet

## 🔹 Working with Linux More Commands
- **ll** – list files in detailed format  
- **touch test1** – create an empty file named `test1`  
- **touch file{1..10}** – create files `file1`, `file2`, ..., `file10`  
- **touch user{1..100}** – create files `user1`, `user2`, ..., `user100`  
- **cd -** – go back to the previous directory  

---

## 🔹 Working with 'head, tail & less' Commands:
- **grep -o root passwd | wc -l** – count occurrences of `root` in `passwd` file  
- **tail passwd | grep root** – search for `root` keyword in the last 10 lines of `passwd`  
- **head passwd | grep root** – search for `root` keyword in the first 10 lines of `passwd`  
- **ll** – list files in detailed format  
- **ll | wc -l** – count the number of items in the current directory  
- **ll /etc | wc -l** – count the number of items in `/etc` directory  
- **cat passwd | wc -l** – count the number of lines in `passwd` file  

---

## 🔹 Working with 'GREP' Command:
- **grep -n root passwd** – search for `root` in `passwd` and show line numbers  

---

## 🔹 Working with Linux 'find' Command:
- **find / -type f -name student** – find files named `student` starting from root directory  
- **find / -type d -name student** – find directories named `student` starting from root directory  
- **find / -size +100M** – find files larger than 100MB starting from root directory  
- **find /var -name mail** – find files or directories named `mail` within `/var` directory  
