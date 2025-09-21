Working with Linux File/Directory permission & owernship:
mkdir linux21
touch file1
ll
d rwxr-xr-x.  2  root  root     6  May 10 17:54  dir1
- rw-r--r--.  1  root  root  2662  May 10 17:55  passwd
- rw-r--r--.  1  root  root     0  May 10 17:54  file1
 
1      2      3   4     5       6          7       8
d rwxr-xr-x.  2  root  root     6  May 10 17:54  dir1
 
1. File type
2. File permission
3. Number of hard link
4. File owner
5. File group
6. File size
7. Date of last modification
8. File name
 
File type:
d - directory
- - regular file
 ### Field no: 2, 4 & 5 (Permission) 
 - subfield 
```
rw-  r--  r--  .  = file1  
  d rwx  r-x  r-x  .  = dir1   
    (u)  (g)  (o) (A)
```
 u = user 
 g = group
 o = others
 A = ACL Permission (.)

 4 = SUID  (s,S)  	- SUID পার্মিশন ব্যবহার হয় Owner ফিল্ডে (1st field) এবং এটা প্রকাশ করা হয় 'S' অথবা 's' দিয়ে।  
 2 = SGID  (s,S) 	- SGID পার্মিশন ব্যবহার হয় Group ফিল্ডে (2nd field) এবং এটাও প্রকাশ করা হয় 'S' অথবা 's' দিয়ে।  
 1 = Sticky bit (t, T)  - Sticky পার্মিশন ব্যবহার হয় Other ফিল্ডে (3rd field) এবং এটা প্রকাশ করা হয় 'T' অথবা 't' দিয়ে।


 - Bydefult file permission = 644
 - Bydefult directory permission = 755
 
- chown mamun file1
- chgrp faculty file1
- chmod 740 file1 
### Linux SUID,SGID, and sticky Bit concept:
**** Special permission (S,s,t,T)

Regular users had access all root partion except /root & /home
### working with SGID
- chmod 770 mydir
- chgrp student mydir
- ls -l mydir
 ```
drwxrwx---.  2  root  student  6  May 10 17:54  mydir
 ```
 - su mamun
 - cd mydir
 - touch file2
 - ls -l
 ```
-rw-rw-r--.  1  mamun  student  0  May 10 17:54  file2
 ```
 - su rahim 
 - cd mydir
 - touch file3
 - ls -l
 ```
-rw-rw-r--.  1  rahim  student  0  May 10 17:54  file3
 ```
 su khalek
 cd mydir
 touch file4
 ls -l
 ```
-rw-rw-r--.  1  khalek  student  0  May 10 17:54  file4
 ```
 
 chmod 2770 mydir
- ls -l mydir
 ```
drwxrws---.  2  root  student  6  May 10 17:54  mydir
 ```
 chmod 2750 mydir
- ls -l mydir
 ```
drwxr-s---.  2  root  student  6  May 10 17:54  mydir
 ```
- umask : when we will create file/folder maximun value dedactedd from 666 & 777
- umask 0022
- umask 0002
- umask 0027
- umask 0077

### working with Sticky bit
Linux directory max permission is 777 . 
- chmod 777 mydir1 : regular permission
- chmod 1777 mydir1 : sticky bit permission
- if you are set sticky bit permission it is not possible to delete other user file from your directory.

### ACL (Access Control List)
getfacl file1
setfacl -m u:rahim:rw file1
setfacl -m u:rahim:--x file1
setfacl -m u:rahim:--- file1
setfacl -x u:rahim file1
setfacl -m g:student:rw file1
setfacl -m o::- file1
setfacl -m m::- file1

### ACL command options:

- m = modify
- x = remove
- b = remove all
- k = remove all default entry
- n = no effect
- M = modify from file
- X = remove from file
- B = remove all from file
- K = remove all default entry from file
- N = no effect from file
# user ACL
- setfacl profile

# group ACL
- groupadd staff
- ***setfacl modify user:username:permission(rwx), others***
- setfacl -m u:mamun:rwx,rose:r--, rahim:--- file1
- setfacl -m g:staff:rw file1
- getfacl tutorial
# Directory Permission:
- mkdir acldir
- touch acldir/file1
- ls -l acldir
-setfacl -R -m u:rahim:rw acldir ; -R = recursive
# ACL add (group)
- setfacl recursivly modify user:username:permission(rwx), others
- setfacl -R -m u:rahim:rw,rose:r--, rahim:--- file1
- getfacl file1
- ls -l file1
# ACL remove (group)
- setfacl -x g:staff file1

# ACL Remove from file:
- setfacl -b tutorial

