# Bandit Level 1 → Level 2

## Level Goal

The password for the next level is stored in a file called - located in the home directory

Actions taken:

Using just cat with spaces in the filename will make it take each word as a separate argument. 
Therefore I used ./ which made the shell treat it as a single file, so it reads it correctly.


``` bash

bandit2@bandit:~$ ls
--spaces in this filename--
bandit2@bandit:~$ cat "./--spaces in this filename--"
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
bandit2@bandit:~$

```
