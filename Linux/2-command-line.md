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

## 🔹 Working with Linux File & Directory Permissions

Example:

    d   rwx rwx  r-x .   2   student student   6    Feb  4 18:06    dir1  
    -   rw- rw-  r-- .   1   student student   0    Feb  4 18:06    file1

### Breakdown of Permissions:

1.  **File/Directory Types** (Column 1):
    -   `-` : Regular file
    -   `d` : Directory
    -   `l` : Symbolic link
    -   `p` : Pipe
    -   `s` : Socket
    -   `c` : Character device
    -   `b` : Block device
2.  **File/Directory Permissions** (Columns 2a, 2b, 2c):
    -   `rwx` : User (owner) permissions: read, write, execute\
    -   `rw-` : Group permissions: read, write\
    -   `r-x` : Other permissions: read, execute\
    -   `.` : Special permissions ACL (Access Control List) like `suid`,
        `sgid`, or sticky bit
3.  **Number of Hard Links** (Column 3)\
4.  **Owner** (Column 4)\
5.  **Group** (Column 5)\
6.  **Size** (Column 6)\
7.  **Date** (Column 7)\
8.  **File Name** (Column 8)

------------------------------------------------------------------------

## 🔹 File/Directory Permission Values:

-   **Read** (r) = 4\
-   **Write** (w) = 2\
-   **Execute** (x) = 1\
-   `-` = no permission\
-   `.` = ACL permission (+)

------------------------------------------------------------------------

## 🔹 Linux File & Directory Types Explained:

-   `-` : Regular file\
-   `d` : Directory (regular directory)\
-   `l` : Symbolic link\
-   `p` : Pipe\
-   `s` : Socket\
-   `c` : Character device (printer, sound card, etc.)\
-   `b` : Block device (hard disk, CD-ROM, USB drive, etc.)
