### Shell Command in Linux
## Types of Linux Shell:
 1. shell sh(.sh)
 2. bash shell (commonly used)
 3. zshell 
 4. cshell (c programming based)
 5. kshell
 6. GNOME (GUI)
 7. KDE (GUI)
### User Defined Variable:
```bash 
    a=10
    echo $a
    echo ${a}
    echo $b
    echo ${b}
    b=20
    echo $b
    echo ${b}
```

### Read from terminal
- `read` a
- `echo` $a

## Example 
```
#!/bin/bash
echo -n " Enter your name" 
read name
echo "Hello, $name !"
sleep 2 
echo " Enter your age "
read age 
echo "your age is $age"
```
## using Conditional Statement:
- `if`
- `elif`
- `else`
- `exit`
- `for`
- `while`
- `until`
- `case`
- `break` 
- `continue`
### working with `IF`
```bash 
echo -n " enter your number"
read num
if test $num -ge 10
then 
echo  " this the number is possitive"
else 
echo " this is the number is negative"
fi
```
## Use of Expression []:
```
echo -n " enter your number"
read num 
if [ $num -ge 0]
then 
echo " this is the number is positive"
else 
echo " this is the number is negative"
fi
```

## working with String
```
echo -n " enter your name"
read name 
if [$user = $LOGNAME]
then 
echo " hello $LOGNAME, welcome to linux"
else
echo "user $user not login in"
fi
```
### System Information using a shell script:
```
#!/bin/bash
clear
echo " ##### $HOSTNAME hardware information ######"
sleep 2
echo "                      "
echo "**********************"
echo "***** system kernel information ****"
uname -r
echo " **************" 
sleep 2
echo " ********system memory info******"
free -m 
echo "******************"
sleep 2
echo "*********HDD information******"
fdisk -l | grep Disk | head -2
echo "*****************"
sleep 2
echo "*********CPU information********"
lscpu | grep "model name"
echo "***************"
sleep 2
echo "*********OS information********"
cat /etc/os-release
echo "***************"
sleep 2
echo "*************"
uptime 

```