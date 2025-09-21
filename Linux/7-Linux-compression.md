## Archives Extraction
- tar -xvf file.tar

## Archive + compress:
 - `-z` : gzip (less)
 - `-j` : bzip2 (more)
 - `-J` : xz (more)
 - `-c` : create
 - `-v` : verbose
 - `-f` : file name
 - `-t` : test
 - `-x` : extract
 - `-z` : gzip
 - `-j` : bzip2
 - `-J` : xz
 - `-p` : preserve permissions

- `bz`: tar -czvf file.tar.gz etc
- `bz2 `: tar -cjvf etc.tar.bz2 etc
- `xz`: tar -cJvf etc.tar.xz etc

## Extract :
- `bz`: tar -xvzf file.tar.gz
- `bz2`: tar -xjvf etc.tar.bz2
- `xz`: tar -xJvf etc.tar.xz
## FIle compression 
- `gzip`: gzip file.txt
- `bzip2`: bzip2 file.txt
- `xz`: xz file.txt

## Extract 
- `gzip`: gunzip file.txt.gz
- `bzip2`: bunzip2 file.txt.bz2
- `xz`: unxz file.txt.xz (old version)