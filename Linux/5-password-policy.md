Rules 1: permit for all
```visudo
```
```
root ALL=(ALL) ALL
mamun ALL=(ALL) ALL
```
### working with /etc/shadow file:
- useradd mamun
- passwd mamun
- chage -d 0 mamun
- chage -l mamun
- chage -m 0 mamun
- chage -M 90 mamun
- chage -W 7 mamun
- chage -E 2020-12-31 mamun
- chage -E -1 mamun
- chage -E 2020-12-31 mamun

```
[root@desktopX ~]# chage -l mamun        ; password related information 'chage -l" 

Last password change                                    : MM DD, YYYY
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7

password: P@ssword123  (new password)
```
```
chage mamun
 Minimum Password age [0]: 3
 Maximum Password age [99999]: 30
 Last Password Changed (YYYY-MM-DD): Press Enter (today)
 Password Expiration Warning [7]: 5 
 Password Inactive [-1]: 5 
 Account Expiration Date (YYYY-MM-DD) [-1]: YYYY-MM-DD

 note: If press Enter account never expire 
 ```
