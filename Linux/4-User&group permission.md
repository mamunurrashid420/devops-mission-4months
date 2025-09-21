# Linux Command Line Cheat Sheet

## 🔹 Working with Linux More Commands

-   **ll** -- list files in detailed format\
-   **touch test1** -- create an empty file named `test1`\
-   **touch file{1..10}** -- create files `file1`, `file2`, ...,
    `file10`\
-   **touch user{1..100}** -- create files `user1`, `user2`, ...,
    `user100`\
-   **cd -** -- go back to the previous directory

------------------------------------------------------------------------

## 🔹 Working with 'head, tail & less' Commands:

-   **grep -o root passwd \| wc -l** -- count occurrences of `root` in
    `passwd` file\
-   **tail passwd \| grep root** -- search for `root` keyword in the
    last 10 lines of `passwd`\
-   **head passwd \| grep root** -- search for `root` keyword in the
    first 10 lines of `passwd`\
-   **ll** -- list files in detailed format\
-   **ll \| wc -l** -- count the number of items in the current
    directory\
-   **ll /etc \| wc -l** -- count the number of items in `/etc`
    directory\
-   **cat passwd \| wc -l** -- count the number of lines in `passwd`
    file

------------------------------------------------------------------------

## 🔹 Working with 'GREP' Command:

-   **grep -n root passwd** -- search for `root` in `passwd` and show
    line numbers

------------------------------------------------------------------------

## 🔹 Working with Linux 'find' Command:

-   **find / -type f -name student** -- find files named `student`
    starting from root directory\
-   **find / -type d -name student** -- find directories named `student`
    starting from root directory\
-   **find / -size +100M** -- find files larger than 100MB starting from
    root directory\
-   **find /var -name mail** -- find files or directories named `mail`
    within `/var` directory

------------------------------------------------------------------------

## 🔹 User and Group Administration

There are three types of users in Linux: 1. **root**: UID `0` 2.
**system**: UID `1 - 999` 3. **normal user**: UID `1000 - 60000`

### Commands for User & Group Checks:

-   **id root** -- check root user ID\
-   **id student** -- check normal user ID\
-   **id mail** -- check system user ID\
-   **id mamun** -- check mamun user ID

### Files for User & Group Information:

-   **tail /etc/passwd** -- list all users\
-   **tail /etc/group** -- list all groups\
-   **tail /etc/shadow** -- list all user passwords (hashed)

Sample entry in `/etc/passwd`:

    mamun: x: 1001: 1001::/home/mamun:/bin/bash

Breaking it down: 1. **User login name** (mamun) 2. **Password** (hashed
`x`) 3. **User ID** (1001) 4. **Group ID** (1001) 5. **Comment** (empty)
6. **Home directory** (/home/mamun) 7. **Default shell** (/bin/bash)

### User Administration Commands:

-   **useradd mamun** -- create the `mamun` user\
-   **useradd test** -- create the `test` user\
-   **passwd mamun** -- set password for the `mamun` user

### user passwords:
- **::** -- password deleted
- **!!** -- password not set
- **!**  -- Locked
- **x** -- password set but encrypted
- **\*::** -- password set but encrypted
