# Bandit Level 12 → Level 13

## Level Goal

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. 
For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name.
Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

Actions taken :

### data 1

Created a tempoary directory with a hard to guess name:
````bash
bandit 12(.2)
bandit12@bandit:~$ mktemp -d
/tmp/tmp.KZ4Q06B6ts
bandit12@bandit:~$
````

Used xxd -r to convert the hex dump back into its original binary form:

`````
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ xxd -r data.txt > data1.bin

`````
Used "file" to check the file type of "data1.bin". As you can see below it's a gzip file.
`````
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ file data1.bin
data1.bin: gzip compressed data, was "data2.bin", last modified: Tue Oct 14 09:26:06 2025, max compression, from Unix, original size modulo 2^32 564
`````
### data 2

Changed the file format to "gz" this so I can de compress with gzip -d command. I followed the same process until
I got a the password.
````
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ mv data1.bin data2.gz
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ gzip -d data2.gz
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ ls
data2  data.txt  zone1.bin
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ file data2
data2: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$

``````
### data 3

`````
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ mv data2 data3.bz2
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ bzip2 -d data3.bz2
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ ls
data3  data.txt  zone1.bin
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ file data3
data3: gzip compressed data, was "data4.bin", last modified: Tue Oct 14 09:26:06 2025, max compression, from Unix, original size modulo 2^32 20480
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$
`````
#### data 4
`````
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ mv data3 data4.gz
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ gzip -d data4.gz
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ ls
data4  data.txt  zone1.bin
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ file data4
data4: POSIX tar archive (GNU)
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$
```````
### data5
```````
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ mv data4 data5.tar
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ tar -xf data5.tar
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ ls
data5.bin  data5.tar  data.txt  zone1.bin
````````
### data 6
````````
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ mv data5.bin data6.tar
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ tar -xf data6.tar
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ ls
data5.tar  data6.bin  data6.tar  data.txt  zone1.bin
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/tmp.KZ4Q06B6ts$
````````

### Password
```````
pwd
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn 
`````````

