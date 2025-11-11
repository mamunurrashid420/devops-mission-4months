LVM we need to comprehend three main components,they are interconnected and together make what we call a Logical Volume thses components are:

1. Physical Volume (PV)
2. Volume Group (VG)
3. Logical Volume (LV)
`Pyhical volume`: These are the base block used to create a LVM, physical volumes or PVs are simply your physical storage devices.
Volume Group: We can think of a volume group VG as a pool that is comprised of physical volumes. Lets say we three 1TB SSD hard drives that are part of a volumes group, this VG will show up as having a consolidated storage capacity of 3TB. WHich will then used to create logical volumes.
Logical Volume: When our VG

## Physical Volume (PV)
- These are the actual Physical storage device- like HDD,SSD,or partitions
- They are the building blocks of LVM
-Each PV is initialized using:
```bash
lsblk
```

```
pvcreate /dev/sdb
```
**Check/Display PV**
```bash
pvs
or 
pvdisplay
```

## Volume Group (VG)
Combine the PVs into a single pool:
```bash
sudo vgcreate my_vg /dev/sdb /dev/sdc
```
check and display
```
vgs
or
vgdisplay
```

## Logical Volume (LV)
Create a logical volume within the VG:
```bash
sudo lvcreate -n my_lv -L 1G my_vg
```
check and display
```bash
lvs
or
lvdisplay
```

## Format and Mount the Logical Volume
Format the LV with a file system (e.g., ext4):
```bash
sudo mkfs.ext4 /dev/my_vg/my_lv
```
Create a mount point and mount the LV:
```bash
sudo mkdir /mnt/my_lv
sudo mount /dev/my_vg/my_lv /mnt/my_lv
```
Verify the mount:
```bash
df -h
```

## Enable AUto-mount on Boot
Add entry to /etc/fstab:
```bash
/dev/my_vg/my_lv /mnt/my_lv ext4 defaults 0 0
```
- Test config
```bash
sudo mount -a
```

## Extend the logical volume
suppose you can more disk space and want to grow the LV:
```
sudo lvextend -L +20G /dev/my_vg/data_lv
sudo resize2fs /dev/my_vg/data_lv
```
Check update size:
```bash
df -h
```
## If you want to remove or clean up 
To remove LV,VG,PV 
```bash
sudo umount /mnt/my_lv
sudo lvremove /dev/my_vg/my_lv
sudo vgremove my_vg
sudo pvremove /dev/sdb /dev/sdc
```
Then 
Check the status removal:
```bash 
sudo pvs
sudo vgs
sudo lvs
```