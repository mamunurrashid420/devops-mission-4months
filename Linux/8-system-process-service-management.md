## Reset Root Password:
- Reboot the system and enter the GRUB menu by pressing the "Esc" key during boot.
- Select the kernel you want to boot into and press "e" to edit the boot parameters.
- Cursor navigate to the end of line tats tarts with `linux`
- Press `END` button to move the cursor to the end of the line.
- Append `rd.break` to the end of the line.
- press `Ctrl+x` to boot using the modified config.

- `switch_root:/#` mount -o remount,rw /sysroot
- `switch_root:/#` chroot /sysroot

- `sh-4.4#` passwd root
- `sh-4.4#` touch /.autorelabel (for selinux) 
- `sh-4.4#` exit
- `switch_root:/#` exit
