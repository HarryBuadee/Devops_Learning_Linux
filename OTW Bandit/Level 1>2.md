# Bandit Level 1 → Level 2

## Level Goal

The password for the next level is stored in a file called - located in the home directory

Actions taken:

Using just cat with spaces in the filename will make it take each word as a separate argument. 
Therefore I used ./ which made the shell treat it as a single file, so it reads it correctly.

- To read the file named -, I used ./- so the shell treats it as a file in the current directory and doesn’t confuse it with stdin.
``` bash

bandit1@bandit:~$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
bandit1@bandit:~$

```
